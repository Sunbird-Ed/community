# Functional Configurations

To configure Sunbird Ed platform based on your use case, you will need to use the Postman tool. You can download and install the Postman tool by visiting the following link: https://www.postman.com/downloads/.

Please refer the below mentioned postman collection to setup minimal functional configuration for content creation workflow.Download the postman collection of Sunbird-Ed functional configuration [https://github.com/project-sunbird/sunbird-ed-installer/blob/release-6.0.0/postman-collection/collectionrelease600.json](https://github.com/project-sunbird/sunbird-ed-installer/blob/release-6.0.0/postman-collection/collectionrelease600.json)

Download the postman environment variable file [https://github.com/project-sunbird/sunbird-ed-installer/blob/release-6.0.0/terraform/azure/template/postman.env.json](https://github.com/project-sunbird/sunbird-ed-installer/blob/release-6.0.0/terraform/azure/template/postman.env.json) and replace the place holder values with actual values.&#x20;

​Import postman collection and environment variables to postman tool

refer: ​[https://learning.postman.com/docs/getting-started/importing-and-exporting-data/#importing-postman-data](https://learning.postman.com/docs/getting-started/importing-and-exporting-data/#importing-postman-data)

* Once the import is done, click on the "Collections" tab located in the upper-left corner. From the dropdown menu in the upper-right corner, select the desired environment name.
* Now, you can start triggering the APIs in the collection one by one, following the specified sequence. Proceed to the next API only when the response from the current API is a successful "200" status code.\


