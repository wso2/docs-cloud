---
template: templates/swagger.html
---

Do the following to try out WSO2 API Cloud's Publisher REST APIs using sample input parameters:     

1.  Expand the relevant API operation and click **Try It Out**.  
2.  Fill in relevant sample values as the input parameters and click **Execute**. You will receive a sample curl command with the sample values you filled in.
3.  Add  a  header to the curl command and run the curl command on the terminal.


  
<div id="swagger-ui"></div>
<script>
window.onload = function() {
  // Begin Swagger UI call region
  const ui = SwaggerUIBundle({
    url: "../../management-apis/restapis/publisher-v1.yaml",
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