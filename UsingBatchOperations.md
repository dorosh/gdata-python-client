Demonstrated using batch requests to perform multiple operations in Google Base.

# Introduction #

I've posted a couple of short code snippets illustrating how to form a batch request for Google Base and Google Spreadsheets. The same general principle applies for other service which support batch requests such as Google Calendar.

# Details #

## Batch Requests ##

Batch requests allow you to send multiple operations in a single HTTP request and may make your software run more quickly by minimizing the number of HTTP requests. To create a batch request, construct a feed with an entry for each operation you would like to perform which includes the desired operation and any entry data which you may need (for example, the new contents which an entry should contain). For more information on batch requests see: http://code.google.com/apis/gdata/batch.html

## Example Code ##
### Google Base ###
The following code assumes that you already have an authenticated client object which is named `gd_client`.
```
# Create two items using a batch request.
request_feed = gdata.base.GBaseItemFeed(atom_id=atom.Id(text='test batch'))
entry1 = gdata.base.GBaseItemFromString('--XML for your new item goes here--')
entry1.title.text = 'first batch request item'
entry2 = gdata.base.GBaseItemFromString('--XML for the second item here--')
entry2.title.text = 'second batch request item'
request_feed.AddInsert(entry1)
request_feed.AddInsert(entry2)
    
result_feed = gd_client.ExecuteBatch(request_feed)

# Now delete the newly created items.
request_feed = gdata.base.GBaseItemFeed(atom_id=atom.Id(text='test deletions'))
request_feed.AddDelete(entry=result_feed.entry[0])
request_feed.AddDelete(entry=result_feed.entry[1])
    
result_feed = self.gd_client.ExecuteBatch(request_feed)
```

### Google Spreadsheets ###
Google Spreadsheets supports batch operations on the cells feed. To change the value of a cell, you perform an update (HTTP PUT) on an existing cell. In this example, I fetch the list of cells in the worksheet then change the values in the first four cells with one HTTP request. The following code assumes that you authenticate the SpreadsheetsService object named `client`.
```
import gdata.spreadsheet
import gdata.spreadsheet.service

client = gdata.spreadsheet.service.SpreadsheetsService()
# Authenticate ...

cells = client.GetCellsFeed('your_spreadsheet_key', wksht_id='your_worksheet_id')

batchRequest = gdata.spreadsheet.SpreadsheetsCellsFeed()

cells.entry[0].cell.inputValue = 'x'
batchRequest.AddUpdate(cells.entry[0])
cells.entry[1].cell.inputValue = 'y'
batchRequest.AddUpdate(cells.entry[1])
cells.entry[2].cell.inputValue = 'z'
batchRequest.AddUpdate(cells.entry[2])
cells.entry[3].cell.inputValue = '=sum(3,5)'
batchRequest.AddUpdate(cells.entry[3])

updated = client.ExecuteBatch(batchRequest, cells.GetBatchLink().href)
```