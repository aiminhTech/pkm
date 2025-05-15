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
- **Example Request**
	- ```xml
	  <?xml version="1.0"?>
	  <ApiRequest xmlns="urn:ige:schema:xsd:datadeliverycore-1.0.0" xmlns:pat="urn:ige:schema:xsd:datadeliverypatent-1.0.0"  xmlns:tmk="urn:ige:schema:xsd:datadeliverytrademark-1.0.0">
	    <Action type="PatentSearch">
	      <pat:PatentSearchRequest xmlns="urn:ige:schema:xsd:datadeliverycommon-1.0.0">
	        <Representation details="Maximal" images="Link" strictness="Strict">
	          <Resource role="item" action="Embed"/>
	          <Resource role="BibliographicData" action="Embed"/>
	          <Resource role="PatentLegalStatusData" action="Embed"/>
	          <Resource role="PatentPublication" action="Embed"/>
	        </Representation>
	        <Page size="50"/>
	        <Query>
	          <And>
	            <pat:PatentNumber>*</pat:PatentNumber>
	          </And>
	        </Query>
	        <Sort>
	          <pat:PatentNumberSort>Descending</pat:PatentNumberSort>
	        </Sort>
	      </pat:PatentSearchRequest>
	    </Action>
	   <Action type="TrademarkSearch">
	      <tmk:TrademarkSearchRequest xmlns="urn:ige:schema:xsd:datadeliverycommon-1.0.0">
	        <Representation details="Maximal" images="Link" strictness="Strict" itemBags="false">
	          <Resource role="item" action="Embed"/>
	        </Representation>
	        <Page size="10"/>
	        <Query>
	          <And>
	            <Id>*</Id>
	          </And>
	        </Query>
	      </tmk:TrademarkSearchRequest>
	    </Action>
	  </ApiRequest>
	  
	  ```
-
-