**Logistic and Supply chain Dashboard**


Column Name	Description	Example Values

ShipmentID	Unique shipment identifier	SHP1001

OrderDate	Date when the order was placed	2024-07-15

ShipDate	Date when the order was shipped	2024-07-17

DeliveryDate	Date when the order was delivered	2024-07-20

OriginCity	Shipment origin	Mumbai

DestinationCity	Shipment destination	Delhi

DistanceKM	Distance between origin and destination (in km)	1420

Carrier	Courier/Shipping partner	BlueDart, DTDC, Delhivery, FedEx

ShipmentMode	Mode of transport	Air, Road, Rail, Sea

ShipmentCost	Total cost of shipment	850

WeightKG	Package weight in kilograms	12.5

DeliveryStatus	Final status of shipment	Delivered, In Transit, Delayed, Cancelled

DelayDays	Number of days delayed (if any)	0, 2, 5

CustomerType	Type of customer	Retail, Wholesale, E-commerce

ProductCategory	Type of goods shipped	Electronics, Apparel, Furniture, FMCG

DeliveryRating	Customer feedback rating (1–5)	4

Warehouse	Warehouse handling the shipment	Mumbai_W1, Delhi_W2

FuelCost	Fuel cost per shipment (if tracked)	120

DriverName	Assigned driver (optional)	Rakesh Kumar

VehicleID	Vehicle registration or ID	MH12AB1234
________________________________________
Changes:
Data cleaning
Date Column format Changed 

****New column added Through power query in power bi to understand time required between order date and delivered date.

Deliverydays = DATEDIFF('logistics_shipping_data_2022_20'[OrderDate],logistics_shipping_data_2022_20[ActualDeliveryDate],DAY)

------------------------------------------------------------------------------------------------------------------------------------------

**Calculated field/New measures added in powerbi powerquery for delivery rate**

Count of ActualDeliveryDate divided by Count of ShipmentID = 

DIVIDE(

	COUNTA('logistics_shipping_data_2022_20'[ActualDeliveryDate]),
	
	COUNTA('logistics_shipping_data_2022_20'[ShipmentID])
	
)

------------------------------------------------------------------------------------------------------------------------------------------------

****Calculated field/New measures added in powerbi powerquery for delivery rate***

Ontimedeliveryrate = DIVIDE (sum(logistics_shipping_data_2022_20[ontimedelivery]),COUNTROWS('logistics_shipping_data_2022_20'),0)

ontimedelivery = if('logistics_shipping_data_2022_20'[DelayDays]=0,1,0)

------------------------------------------------------------------------------------------------------------------------------------------------


Analysis Power BI Dashboard:

1.	Delivery Performance
o	Total Orders received and order status
o	Total shipment cost
o	City slicer added
o	Average of delivery days by shipment days
o	Average of shipment Cost by Distance KM
o	Average of shipment cost by Shipment mode
o	Average of shipment cost by carrier

Findings:  

•	Roadways required time to deliver comparatively air ways deliver in lesser time however airways are expensive than other modes it then increases Shipment cost.
•	when the distance increase shipment cost also increases.
•	Ecom express are expensive and DTDC are cheaper.

3.	Customer insights
o	City wise order count and rating
o	Sum of delivery rating by carrier
o	Frequently ordered 
o	Rating by customer type
o	Delivery rating by number of days order delayed
o	Rating slicer

Findings:  

•	Received the highest order from Chennai with the highest positive ratings
•	Delivery rating also defers on the basis carrier DTDC with the highest rating and bluedart get the lowest.
•	The Highest order received are from FMCG.
•	Retail segment with the positive rating and e-commerce segment is at the bottom.
•	Customer rating and satisfaction is mainly linked to the estimated delivery time; I can see the      on-time delivery has the highest rating and customer satisfaction.

5.	KPI
o	On time delivery rate
o	Average of delay days
o	Average of shipment cost
o	Count of Delivery status
o	Scatterplot - Sum of Distance Km and sum of shipment cost by product category
