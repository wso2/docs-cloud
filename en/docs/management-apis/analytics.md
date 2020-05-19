---
template: templates/swagger.html
---

You need to have a paid plan to use the analytics REST API.  

If you are on a trial account, first you should upgrade to a [preferred pricing plan](https://wso2.com/api-management/cloud/#pricing). Once you are on a paid plan and you want to use the analytics REST API, you need to contact us via a support ticket to obtain required tokens to invoke the APIs. 
When you contact us, we will generate the required tokens and share with you so that you can start using the analytics REST API.

**NOTE**: There is a limitation of 5 API calls per minute for each token.

Do the following to try out the REST APIs using sample input parameters:     

1.  Expand the relevant API operation and click the **Try It Out** button.  
2.  Fill in relevant sample values for the input parameters and click **Execute**. You will receive a sample curl command with the sample values you filled in.
3.  Add  a  header to the curl command and run the curl command on the terminal.




  
<div id="swagger-ui"></div>
<script>
window.onload = function() {
  // Begin Swagger UI call region
  const ui = SwaggerUIBundle({
    url: "../../management-apis/restapis/analytics.yaml",
    dom_id: '#swagger-ui',
    deepLinking: true,
    validatorUrl: null,
    presets: [
      SwaggerUIBundle.presets.apis,
      SwaggerUIStandalonePreset
    ],
    plugins: [
      SwaggerUIBundle.plugins.DownloadUrl
    ],
    layout: "StandaloneLayout"
  })
  // End Swagger UI call region

  window.ui = ui
}
</script>