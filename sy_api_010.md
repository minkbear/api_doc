---


---

<h1 id="introduction-shipyous-api-v1-updated-on-2572018-1620">Introduction Shipyous API v1 (updated on 25/7/2018 16:20)</h1>
<p>Shipyours API enable you to manage data on server through REST API.</p>
<p>Please reach out directly to <a href="mailto:itmanager@outsourcingfactory.co.th">itmanager@outsourcingfactory.co.th</a> for URI, Token.</p>
<h1 id="authentication">Authentication</h1>
<p>Shipyours uses Bearer Token in which you can acquire the token by sending an inquiry email to <a href="mailto:itmanager@outsourcingfactory.co.th">itmanager@outsourcingfactory.co.th</a> (please also specify your customer code within the email).</p>
<p>Shipyours will reply back with Bearer Token, in which it can be used in the next topic.</p>
<p>Note: Bearer Token can only be used on a single project.</p>
<h1 id="headers">Headers</h1>
<p>Please ensure to use below header format for every request.</p>
<p><code>Accept: application/json</code></p>
<p><code>Content-Type: application/json</code></p>
<p><code>Authorization: Bearer API_KEY_HERE</code></p>
<h1 id="errors">Errors</h1>
<p>Shipyous API uses conventional HTTP response codes to indicate the success or failure of an API request. The table below contains a summary of the typical response codes:</p>

<table>
<thead>
<tr>
<th>Code</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr>
<td>200</td>
<td>Normal</td>
</tr>
<tr>
<td>401</td>
<td>Permission denied because of no Token</td>
</tr>
<tr>
<td>404</td>
<td>The request resource could not be found.</td>
</tr>
<tr>
<td>422</td>
<td>Incorrect or Insufficient Parameters.</td>
</tr>
<tr>
<td>500</td>
<td>Internal error in Shipyours API (please notify us)</td>
</tr>
<tr>
<td>503</td>
<td>Shipyous API is offline for maintenance.</td>
</tr>
</tbody>
</table><h2 id="response-sample">401: Response Sample</h2>
<pre class=" language-json"><code class="prism  language-json"><span class="token punctuation">{</span>
    <span class="token string">"message"</span><span class="token punctuation">:</span> <span class="token string">"401 Unauthorized"</span><span class="token punctuation">,</span>
    <span class="token string">"status_code"</span><span class="token punctuation">:</span> <span class="token number">401</span>
<span class="token punctuation">}</span>
</code></pre>
<h2 id="response-sample-1">404: Response Sample</h2>
<pre class=" language-json"><code class="prism  language-json"><span class="token punctuation">{</span>
    <span class="token string">"message"</span><span class="token punctuation">:</span> <span class="token string">"404 Not Found"</span><span class="token punctuation">,</span>
    <span class="token string">"status_code"</span><span class="token punctuation">:</span> <span class="token number">404</span>
<span class="token punctuation">}</span>
</code></pre>
<h2 id="response-sample-2">422: Response Sample</h2>
<pre class=" language-json"><code class="prism  language-json"><span class="token punctuation">{</span>
    <span class="token string">"message"</span><span class="token punctuation">:</span> <span class="token string">"422 Unprocessable Entity"</span><span class="token punctuation">,</span>
    <span class="token string">"errors"</span><span class="token punctuation">:</span> <span class="token punctuation">{</span>
        <span class="token string">"schedule_deliver_date"</span><span class="token punctuation">:</span> <span class="token punctuation">[</span>
            <span class="token string">"The schedule deliver date does not match the format Y-m-d."</span>
        <span class="token punctuation">]</span>
    <span class="token punctuation">}</span><span class="token punctuation">,</span>
    <span class="token string">"status_code"</span><span class="token punctuation">:</span> <span class="token number">422</span>
<span class="token punctuation">}</span>
</code></pre>
<h2 id="response-sample-3">500: Response Sample</h2>
<pre class=" language-json"><code class="prism  language-json"><span class="token punctuation">{</span>
    <span class="token string">"message"</span><span class="token punctuation">:</span> <span class="token string">"..."</span><span class="token punctuation">,</span>
    <span class="token string">"status_code"</span><span class="token punctuation">:</span> <span class="token number">500</span>
<span class="token punctuation">}</span>
</code></pre>
<h1 id="orders">Orders</h1>
<h2 id="create-an-order">Create an order</h2>
<h3 id="http-request">HTTP Request</h3>
<p><code>POST /api/v1/order</code></p>
<h3 id="parameters">Parameters</h3>

<table>
<thead>
<tr>
<th>Key</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr>
<td>schedule_deliver_date</td>
<td>Shipping date in yyyy-mm-dd format (2018-07-20)</td>
</tr>
<tr>
<td>schedule_deliver_time</td>
<td>Desired shipping time in hh:mm (24H) format (17:20)</td>
</tr>
<tr>
<td>rc_name</td>
<td>Reciever’s name</td>
</tr>
<tr>
<td>rc_address1</td>
<td>Reciever’s address 1 (line 1)</td>
</tr>
<tr>
<td>rc_address2</td>
<td>Reciever’s address (sub district)</td>
</tr>
<tr>
<td>rc_address3</td>
<td>Reciever’s address 3 (district)</td>
</tr>
<tr>
<td>rc_country</td>
<td>Destination country (see valid list in Reference &gt; Country )</td>
</tr>
<tr>
<td>rc_postcode</td>
<td>Zip code</td>
</tr>
<tr>
<td>rc_phone</td>
<td>Telephone number</td>
</tr>
<tr>
<td>rc_email</td>
<td>Email</td>
</tr>
<tr>
<td>cod_amount</td>
<td>Cash on delivery amount to be collected</td>
</tr>
<tr>
<td>remark</td>
<td>Remark</td>
</tr>
<tr>
<td>ref1</td>
<td>Reference 1</td>
</tr>
<tr>
<td>ref2</td>
<td>Reference 2</td>
</tr>
<tr>
<td>carrier_method_code</td>
<td>Shipping method</td>
</tr>
</tbody>
</table><p>(see detail in Reference &gt; Carrier Method Code)<br>
items | See more detail in Reference &gt; Item Object</p>
<h3 id="sample-request">Sample Request</h3>
<pre class=" language-json"><code class="prism  language-json"><span class="token punctuation">{</span>
	<span class="token string">"schedule_deliver_date"</span><span class="token punctuation">:</span> <span class="token string">"2018-05-31"</span><span class="token punctuation">,</span>
	<span class="token string">"schedule_deliver_time"</span><span class="token punctuation">:</span> <span class="token string">""</span><span class="token punctuation">,</span>
	<span class="token string">"rc_name"</span><span class="token punctuation">:</span> <span class="token string">"ทดสอบ"</span><span class="token punctuation">,</span>
	<span class="token string">"rc_address1"</span><span class="token punctuation">:</span> <span class="token string">"ทดสอบ"</span><span class="token punctuation">,</span>
	<span class="token string">"rc_address2"</span><span class="token punctuation">:</span> <span class="token string">"ทดสอบ"</span><span class="token punctuation">,</span>
	<span class="token string">"rc_address3"</span><span class="token punctuation">:</span> <span class="token string">"ทดสอบ"</span><span class="token punctuation">,</span>
	<span class="token string">"rc_country"</span><span class="token punctuation">:</span> <span class="token string">"Thailand"</span><span class="token punctuation">,</span>
	<span class="token string">"rc_postcode"</span><span class="token punctuation">:</span> <span class="token string">"10600"</span><span class="token punctuation">,</span>
	<span class="token string">"rc_phone"</span><span class="token punctuation">:</span> <span class="token string">"0851234567"</span><span class="token punctuation">,</span>
	<span class="token string">"rc_email"</span><span class="token punctuation">:</span> <span class="token string">""</span><span class="token punctuation">,</span>
	<span class="token string">"cod_amount"</span><span class="token punctuation">:</span> <span class="token string">""</span><span class="token punctuation">,</span>
	<span class="token string">"remark"</span><span class="token punctuation">:</span> <span class="token string">""</span><span class="token punctuation">,</span>
	<span class="token string">"ref1"</span><span class="token punctuation">:</span> <span class="token string">""</span><span class="token punctuation">,</span>
	<span class="token string">"ref2"</span><span class="token punctuation">:</span> <span class="token string">""</span><span class="token punctuation">,</span>
	<span class="token string">"carrier_method_code"</span><span class="token punctuation">:</span> <span class="token string">"TP1"</span><span class="token punctuation">,</span>
	<span class="token string">"items"</span><span class="token punctuation">:</span> <span class="token punctuation">{</span><span class="token string">"sku-01"</span><span class="token punctuation">:</span><span class="token string">"2"</span><span class="token punctuation">,</span><span class="token string">"sku-01"</span><span class="token punctuation">:</span><span class="token string">"1"</span><span class="token punctuation">}</span>
<span class="token punctuation">}</span>
</code></pre>
<h3 id="sample-response">Sample Response</h3>
<pre class=" language-json"><code class="prism  language-json"><span class="token punctuation">{</span>
    <span class="token string">"success"</span><span class="token punctuation">:</span> <span class="token boolean">true</span><span class="token punctuation">,</span>
    <span class="token string">"data"</span><span class="token punctuation">:</span> <span class="token punctuation">{</span>
        <span class="token string">"code"</span><span class="token punctuation">:</span> <span class="token string">"E0-1807-1172"</span><span class="token punctuation">,</span>
        <span class="token string">"status"</span><span class="token punctuation">:</span> <span class="token string">"WAIT_FOR_PROCESSING"</span><span class="token punctuation">,</span>
        <span class="token string">"schedule_deliver_date"</span><span class="token punctuation">:</span> <span class="token string">"2018-05-31"</span><span class="token punctuation">,</span>
        <span class="token string">"schedule_deliver_time"</span><span class="token punctuation">:</span> <span class="token string">"00:00:00"</span><span class="token punctuation">,</span>
        <span class="token string">"weight_g"</span><span class="token punctuation">:</span> <span class="token number">0</span><span class="token punctuation">,</span>
        <span class="token string">"tracking_number"</span><span class="token punctuation">:</span> <span class="token string">""</span><span class="token punctuation">,</span>
        <span class="token string">"carrier_method_code"</span><span class="token punctuation">:</span> <span class="token string">"TP1"</span><span class="token punctuation">,</span>
        <span class="token string">"cod_amount"</span><span class="token punctuation">:</span> <span class="token number">0</span><span class="token punctuation">,</span>
        <span class="token string">"rc_name"</span><span class="token punctuation">:</span> <span class="token string">"ทดสอบ"</span><span class="token punctuation">,</span>
        <span class="token string">"rc_address1"</span><span class="token punctuation">:</span> <span class="token string">"ทดสอบ"</span><span class="token punctuation">,</span>
        <span class="token string">"rc_address2"</span><span class="token punctuation">:</span> <span class="token string">"ทดสอบ"</span><span class="token punctuation">,</span>
        <span class="token string">"rc_address3"</span><span class="token punctuation">:</span> <span class="token string">"ทดสอบ"</span><span class="token punctuation">,</span>
        <span class="token string">"rc_postcode"</span><span class="token punctuation">:</span> <span class="token string">"10600"</span><span class="token punctuation">,</span>
        <span class="token string">"rc_country"</span><span class="token punctuation">:</span> <span class="token string">"Thailand"</span><span class="token punctuation">,</span>
        <span class="token string">"rc_phone"</span><span class="token punctuation">:</span> <span class="token string">"0851234567"</span><span class="token punctuation">,</span>
        <span class="token string">"rc_email"</span><span class="token punctuation">:</span> <span class="token string">""</span><span class="token punctuation">,</span>
        <span class="token string">"remark"</span><span class="token punctuation">:</span> <span class="token string">""</span><span class="token punctuation">,</span>
        <span class="token string">"ref1"</span><span class="token punctuation">:</span> <span class="token string">""</span><span class="token punctuation">,</span>
        <span class="token string">"ref2"</span><span class="token punctuation">:</span> <span class="token string">""</span><span class="token punctuation">,</span>
        <span class="token string">"items"</span><span class="token punctuation">:</span> <span class="token punctuation">[</span>
            <span class="token punctuation">{</span>
                <span class="token string">"sku_code"</span><span class="token punctuation">:</span> <span class="token string">"sku-01"</span><span class="token punctuation">,</span>
                <span class="token string">"qty"</span><span class="token punctuation">:</span> <span class="token number">2</span>
            <span class="token punctuation">}</span><span class="token punctuation">,</span>
            <span class="token punctuation">{</span>
                <span class="token string">"sku_code"</span><span class="token punctuation">:</span> <span class="token string">"sku-02"</span><span class="token punctuation">,</span>
                <span class="token string">"qty"</span><span class="token punctuation">:</span> <span class="token number">1</span>
            <span class="token punctuation">}</span>
        <span class="token punctuation">]</span>
    <span class="token punctuation">}</span><span class="token punctuation">,</span>
    <span class="token string">"message"</span><span class="token punctuation">:</span> <span class="token string">"Orders saved successfully"</span>
<span class="token punctuation">}</span>
</code></pre>
<h2 id="get-an-order">Get an order</h2>
<h3 id="http-request-1">HTTP Request</h3>
<p><code>GET /api/v1/order/ORDER_CODE_HERE</code></p>
<p>ex. <code>GET /api/v1/order/E0-1801-0001</code></p>
<h3 id="sample-response-1">Sample Response</h3>
<pre class=" language-json"><code class="prism  language-json"><span class="token punctuation">{</span>
    <span class="token string">"success"</span><span class="token punctuation">:</span> <span class="token boolean">true</span><span class="token punctuation">,</span>
    <span class="token string">"data"</span><span class="token punctuation">:</span> <span class="token punctuation">{</span>
        <span class="token string">"code"</span><span class="token punctuation">:</span> <span class="token string">"E0-1806-4951"</span><span class="token punctuation">,</span>
        <span class="token string">"status"</span><span class="token punctuation">:</span> <span class="token string">"DONE"</span><span class="token punctuation">,</span>
        <span class="token string">"schedule_deliver_date"</span><span class="token punctuation">:</span> <span class="token string">"2018-06-29"</span><span class="token punctuation">,</span>
        <span class="token string">"schedule_deliver_time"</span><span class="token punctuation">:</span> <span class="token string">""</span><span class="token punctuation">,</span>
        <span class="token string">"weight_g"</span><span class="token punctuation">:</span> <span class="token number">109</span><span class="token punctuation">,</span>
        <span class="token string">"tracking_number"</span><span class="token punctuation">:</span> <span class="token string">"TEST123456"</span><span class="token punctuation">,</span>
        <span class="token string">"carrier_method_code"</span><span class="token punctuation">:</span> <span class="token string">"SY1"</span><span class="token punctuation">,</span>
        <span class="token string">"cod_amount"</span><span class="token punctuation">:</span> <span class="token number">1190</span><span class="token punctuation">,</span>
        <span class="token string">"rc_name"</span><span class="token punctuation">:</span> <span class="token string">"test"</span><span class="token punctuation">,</span>
        <span class="token string">"rc_address1"</span><span class="token punctuation">:</span> <span class="token string">"test test"</span><span class="token punctuation">,</span>
        <span class="token string">"rc_address2"</span><span class="token punctuation">:</span> <span class="token string">""</span><span class="token punctuation">,</span>
        <span class="token string">"rc_address3"</span><span class="token punctuation">:</span> <span class="token string">""</span><span class="token punctuation">,</span>
        <span class="token string">"rc_postcode"</span><span class="token punctuation">:</span> <span class="token string">"84130"</span><span class="token punctuation">,</span>
        <span class="token string">"rc_country"</span><span class="token punctuation">:</span> <span class="token string">"Thailand"</span><span class="token punctuation">,</span>
        <span class="token string">"rc_phone"</span><span class="token punctuation">:</span> <span class="token string">"02123456789"</span><span class="token punctuation">,</span>
        <span class="token string">"rc_email"</span><span class="token punctuation">:</span> <span class="token string">""</span><span class="token punctuation">,</span>
        <span class="token string">"remark"</span><span class="token punctuation">:</span> <span class="token string">"รับสินค้า 29/6/18"</span><span class="token punctuation">,</span>
        <span class="token string">"ref1"</span><span class="token punctuation">:</span> <span class="token string">"123456"</span><span class="token punctuation">,</span>
        <span class="token string">"ref2"</span><span class="token punctuation">:</span> <span class="token string">""</span><span class="token punctuation">,</span>
        <span class="token string">"items"</span><span class="token punctuation">:</span> <span class="token punctuation">[</span>
            <span class="token punctuation">{</span>
                <span class="token string">"sku_code"</span><span class="token punctuation">:</span> <span class="token string">"sku-01"</span><span class="token punctuation">,</span>
                <span class="token string">"qty"</span><span class="token punctuation">:</span> <span class="token number">1</span>
            <span class="token punctuation">}</span>
        <span class="token punctuation">]</span>
    <span class="token punctuation">}</span><span class="token punctuation">,</span>
    <span class="token string">"message"</span><span class="token punctuation">:</span> <span class="token string">"Orders retrieved successfully"</span>
<span class="token punctuation">}</span>
</code></pre>
<h1 id="reference">Reference</h1>
<h2 id="item-object">Item Object</h2>
<p>Item object is JSON object that that identify an SKU and shipping quantity.<br>
“Key” is an SKU code while “Value” is desired quantity.</p>
<p>ex.</p>
<pre class=" language-json"><code class="prism  language-json"><span class="token punctuation">{</span>
	<span class="token string">"sku_01"</span><span class="token punctuation">:</span><span class="token string">"1"</span><span class="token punctuation">,</span>
	<span class="token string">"sku_02"</span><span class="token punctuation">:</span><span class="token string">"1"</span><span class="token punctuation">,</span>
	<span class="token string">"sku_03"</span><span class="token punctuation">:</span><span class="token string">"1"</span>
<span class="token punctuation">}</span>
</code></pre>
<h2 id="order-status-code">Order Status Code</h2>

<table>
<thead>
<tr>
<th>Key</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr>
<td>WAIT_FOR_PROCESSING</td>
<td>Processing</td>
</tr>
<tr>
<td>WAIT_FOR_PICK</td>
<td>Waiting for pick</td>
</tr>
<tr>
<td>WAIT_FOR_CAL_SHIPPING_COST</td>
<td>Waiting for shipping cost to be calculated</td>
</tr>
<tr>
<td>WAIT_FOR_DELIVER</td>
<td>Waiting to dispatch</td>
</tr>
<tr>
<td>WAIT_FOR_RESULT</td>
<td>Waiting for shipping confirmation</td>
</tr>
<tr>
<td>DONE</td>
<td>Sent</td>
</tr>
<tr>
<td>CANCEL</td>
<td>Cancelled</td>
</tr>
<tr>
<td>POSTPONE</td>
<td>Postpone</td>
</tr>
</tbody>
</table><h2 id="carrier-method-code">Carrier Method Code</h2>

<table>
<thead>
<tr>
<th>Key</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr>
<td>TP1</td>
<td>EMS</td>
</tr>
<tr>
<td>TP2</td>
<td>Registered</td>
</tr>
<tr>
<td>TP3</td>
<td>Int’l Small Packet-Air</td>
</tr>
<tr>
<td>TP4</td>
<td>Parcel</td>
</tr>
<tr>
<td>TP5</td>
<td>Registered Int’l Small Packet-Air</td>
</tr>
<tr>
<td>TP6</td>
<td>International EMS</td>
</tr>
<tr>
<td>DH1</td>
<td>DHL Express</td>
</tr>
<tr>
<td>SY1</td>
<td>Warehouse Pickup</td>
</tr>
<tr>
<td>AL1</td>
<td>Alpha</td>
</tr>
<tr>
<td>KR1</td>
<td>KERRY</td>
</tr>
<tr>
<td>OF1</td>
<td>MESSENGER</td>
</tr>
<tr>
<td>SP1</td>
<td>Shoppee (pickup)</td>
</tr>
<tr>
<td>LZ1</td>
<td>LAZADA (pickup)</td>
</tr>
<tr>
<td>ES1</td>
<td>11street (pickup)</td>
</tr>
<tr>
<td>SS1</td>
<td>Season (pickup)</td>
</tr>
<tr>
<td>DHC</td>
<td>DHL TH</td>
</tr>
</tbody>
</table><h2 id="country">Country</h2>
<p>Please go to <a href="https://gist.github.com/kalinchernev/486393efcca01623b18d">https://gist.github.com/kalinchernev/486393efcca01623b18d</a></p>

