# notes
# docauth startup 
pm2 start /root/.nvm/versions/node/v8.11.3/bin/http-server --name docauth -- -p 3001 -d false


.es(metric='sum:totalAmount').label('Current Year') ,
.es(metric='sum:totalAmount',offset=-1y).label('lPrevious Year') ,


// scripted field 
doc['orderCD'].date.dayOfWeek + " (" + ["", "Mon", "Tue", "Wed", "Thu", "Fri", "Sat", "Sun"][doc['orderCD'].date.dayOfWeek] + ")"


// create directories
require('./createDir');
// set environment variables first
require('./envVars');
// set globals
require('./globals');
var mongooseMulti = require('mongoose-multi');

const {
    mongoose
} = require('./config');

var config = require('./config').aleenaMongo, // external network file
schemaFile = require('./aleenaschema/index');  // external schema file


var connections = {};
for (var databaseName in config.db) {
   connections[databaseName] = {
      name: databaseName,
      url: config.db[databaseName],
      schemas: schemaFile[databaseName]
      // options : null - not implemented yet
   };
}

// start the connections
var aleenaDB = mongooseMulti.start(connections,schemaFile);

global.aleenaDB = aleenaDB;

global.aleenaDB.aleena_dev.financialaccount.find({
   
}).exec(function (err, docs) {
    // do sth. here with customers
    console.log(docs)
});

mongoose.init(() => {
    if (options.exportmongo) {
        // fetch mongodump 
        require('./mongodump');
    }
    if (options.elasticimport) {
        require('./importtoelastic');
        require('./process');
    }
})

// uncaughtException Exception notification sent to Slack channel
process.on('uncaughtException', (err) => {
    mongoose.disconnectM();

    logger.error((new Date).toUTCString() + ' uncaughtException:', err.message);
    logger.error(err.stack);
    process.exit(1);
});

process.on("unhandledRejection", error => {
    mongoose.disconnectM();

    // Will print "unhandledRejection err is not defined"
    console.log("unhandledRejection", error.message);
});
