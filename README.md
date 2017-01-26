Pay2
====
VoguePay Payment Processor Extension for Yii2 Framework (Command API is in beta).


Installation
------------

The preferred way to install this extension is through [composer](http://getcomposer.org/download/).

Either run

```
composer require --prefer-dist tecsin/yii2-voguepay "*"
```

or add

```
"tecsin/yii2-voguepay": "*"
```

to the require section of your `composer.json` file.


Usage
-----

First set up the database by running the migration code :

```
php yii migrate --migrationPath="@vendor/tecsin/yii2-voguepay/migrations"
```

Mobile/Server-to-Server
-----

You can either send user to VoguePay payment page directly (this is the default):

```php
    $MsModel = Yii::createObject(\tecsin\pay2\models\VoguepayMs::className(), ['aaaMerchantId' => '11111', 'mmmMemo' => 'one sparklyn yellow wedding dress', 'tttTotalCost' => '200310', 'rrrMerchantRef' => time().mt_rand(0,999999999)]);
    if($MsModel->validate()){
       return $MsModel->setRequest()->sendRequest()->sendResponse();
    } 
```

Or show the user a pay button (set showPayButton property to true):

```php
    $MsModel = Yii::createObject(\tecsin\pay2\models\VoguepayMs::className(), ['aaaMerchantId' => '11111', 'mmmMemo' => 'one sparklyn yellow wedding dress', 'tttTotalCost' => '200310', 'rrrMerchantRef' => time().mt_rand(0,999999999), 'showPayButton' => true]);
    if($MsModel->validate()){
        $response =  $MsModel->setRequest()->sendRequest()->sendResponse();
        return $response;//response is json {status: "success|error", success|error : { message: "https://www.voguepay.com/payment-url|errorMesssge"}}
    } 
```

Command API
-----

With the Command API you can Fetch records of transactions, Pay (send money) to VoguePay merchants, Withdraw money to various bank accounts, and create a new user on VoguePay.


See [VoguePay](https://voguepay.com/developers) Developer Page

TODO
-----

Add user interface for management.

Create a comprehensive documentation.
