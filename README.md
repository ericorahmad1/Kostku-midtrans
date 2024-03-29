# Kostku-midtrans

This is final project payment midtrans serverless PHP using Heroku

# Description

This is a example mobile SDK server for Midtrans's iOS and Android SDK, as an implementation reference to use the mobile sdk. Please read more in Documentation of Midtrans mobile SDK.
Purpose

The main idea why this server implementation needed is: To securely add HTTP Authorization Header from server side. This auth header is generated from server key (from your Midtrans account), this server key is secret, and should only be kept in server side, not client side (mobile app can be easily reverse engineered to extract any secret).

Additionally, it allows you to tweak JSON request parameter as needed from server side.
Endpoints

There is only one endpoint that are required to use Midtrans mobile SDK:

POST /charge/

This endpoint will proxy (forward) client request to Midtrans Snap API 'https://app.midtrans.com/snap/v1/transactions' (or 'https://app.sandbox.midtrans.com/snap/v1/transactions' for sandbox) with HTTP Authorization Header generated based on your Midtrans Server Key.

The response of API will be printed/returned to client as is. Example response that will be printed

{
    "token": "413ae932-471d-4c41-bfb4-e558cc271dcc",
    "redirect_url": "https://app.sandbox.midtrans.com/snap/v2/vtweb/413ae932-471d-4c41-bfb4-e558cc271dcc"
}

# Usage

Edit file charge/index.php, insert your Midtrans Account Server Key to '<server key>'. Upload these to your host, and make sure the url <url where you host this>/charge/index.php can be accessed from the mobile app.

Set <url where you host this>/charge/index.php as merchant base url in mobile SDK. (refer to Midtrans mobile SDK doc)

    Advanced Tips: You can also configure your HTTP server to route <url where you host this>/charge/ url to /charge/index.php file. So the merchant base url can be just configured as <url where you host this>/(without charge/index.php, because SDK will automatically convert it to <url where you host this>/charge/ then your server will route to /charge/index.php/).


=======

