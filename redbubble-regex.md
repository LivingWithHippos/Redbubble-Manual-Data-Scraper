To keep this script simple all I used was the website http://regexr.com/ 

Open a new page there and delete everything in the "Expression" and "Text" fields. 
Open a new page to https://www.redbubble.com/account/sales/by_sale (you need to be logged in) and right click -> see page source (or whatever it's called in your browser) and copy everything. Paste it in the "Text" field you previously deleted. You'll need to do this for every page (I don't have many sales so it was doable). Copy and paste this string in the "Expression" field:
```
<tr>[^<]+<td>([^<]+)<\/td>[^<]+<td>([^<]+)<\/td>[^<]+<td>[^<]+<a href="([^"]+)">([^<]+)<\/a>[^<]+<\/td>[^<]+<td>([^<]+)<\/td>[^<]+<td>([^<]+)<\/td>[^<]+<td>([^<]+)<\/td>[^<]+<td>([^<]+)<\/td>[^<]+<td>([^<]+)<\/td>[^<]+<td>[\s]*(<a href[^>]+>)?([\w ]+)(<\/a>)?[\s]*<\/td>[^<]+<td>([^<]+)<\/td>[^<]+<td[^>]+>([^<]+)<\/td>[^<]+<td[^>]+>([^<]+)<\/td>[^<]+<td[^>]+>([^<]+)<\/td>[^<]+<\/tr>
```
Now press "List" on the bottom of the regexr.com page and copy and paste this String to obtain a report-like syntax:
```
Order Date: $1\nShip Date: $2\nWork: $3\nName: $4\nOrder #: $5\nProduct: $6\nFulfillment Country: $7\nDestination Country: $8\nDestination State: $9\nStatus: $10\nQty: $11\nRetail Price: $12\nManufacturing Fee: $13\nArtist Margin: $14\n---------------\n
```
You can copy and paste the result where you want. You can easly remove or change order of your output elements, they're the $NUMBER ones in the second regex (e.g. $6 is the product).

If you want to create a CSV-compatible file create a new .csv file and put this at its top to give your columns a title
```
Order Date;Ship Date;Work;Order #;Product;Fulfillment Country;Destination Country;Destination State;Status;Quantity;Retail Price;Manufacturing Fee;Artist Margin
```
now put this string in the "List" field on regexr.com
```
$1;$2;"$4";$5;$6;$7;$8;$9;$11;$13;$14;$15;$16\n
```
copy and paste your result to the CSV file under the first row. 

## Importing to Excel/Calc, Issues

If you encounter strange characters like `&#39;` you can replace them 

| HTML | replace with |
| --- | --- |
| `&#39;` | ' |
| `&amp;` | & | 

I used ; as separators in the CSV so if any of your results has a ";" it's going to break your import, but the "" I've put $4 in should have fixed this.

You can replace the "." with "," in the earnings cell to make them recognized as numbers if you have such layout.

Set the date columns as date when importing them.

???

Profit.



