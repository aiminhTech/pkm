- https://issues.ipip.ch/browse/LRN-276
-
-
- **DataDelivery Test Request mit mehreren Continuations**
	- [https://dev-www.swissreg.ch/public/apidocs/reference/actions.html#echo-action](https://dev-www.swissreg.ch/public/apidocs/reference/actions.html#echo-action)
	- ```xml
	  <?xml version="1.0" encoding="UTF-8"?>	
	  <ApiRequest xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:schemaLocation="urn:ige:schema:xsd:datadeliverycore-1.0.0 urn:publicid:-:IGE:XSD+DATADELIVERYCORE+1.0.0:EN
	      http://www.w3.org/1999/xhtml http://www.w3.org/2002/08/xhtml/xhtml1-strict.xsd"
	      xmlns="urn:ige:schema:xsd:datadeliverycore-1.0.0">
	  
	      <Action type="Echo">
	          <script xmlns="http://www.w3.org/1999/xhtml" type="dbg">AGAIN=c1! AGAIN=c2!</script>
	      </Action>
	  
	      <Action type="Echo">
	          <script xmlns="http://www.w3.org/1999/xhtml" type="dbg">AGAIN=cX!</script>
	      </Action>
	  
	  </ApiRequest>
	  
	  ```
-