# notes
# docauth startup 
pm2 start /root/.nvm/versions/node/v8.11.3/bin/http-server --name docauth -- -p 3001 -d false


.es(metric='sum:totalAmount').label('Current Year') ,
.es(metric='sum:totalAmount',offset=-1y).label('lPrevious Year') ,


// scripted field 
doc['orderCD'].date.dayOfWeek + " (" + ["", "Mon", "Tue", "Wed", "Thu", "Fri", "Sat", "Sun"][doc['orderCD'].date.dayOfWeek] + ")"
