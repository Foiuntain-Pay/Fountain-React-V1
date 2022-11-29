<p align="center">
    <img title="Fountainpay" height="200" src="https://fountainpay.ng/static/media/logo.ae427b76c4cf99998a6be8c0cc1336f6.svg" width="50%"/>
</p>

# Fountainpay-v1 React Library
![Publish React Package](https://github.com/Foiuntain-Pay/Fountainpay-React-v1/workflows/Publish%20React%20Package/badge.svg)
![npm](https://img.shields.io/badge/Fountain-pay-red)
![npm](https://img.shields.io/badge/Fountain-pay-red)
![NPM](https://img.shields.io/badge/Fountain-pay-red)



## Introduction

The React SDK helps you create seamless payment experiences in your React mobile or web app. By connecting to our modal, you can start collecting payment in no time.

Available features include:

- Collections: Card, Account, Mobile money, Bank Transfers, NQR.
- Recurring payments: Tokenization and Subscriptions.
- Split payments


## Table of Contents

1. [Requirements](#requirements)
2. [Installation](#installation)
3. [Initialization](#initialization)
4. [Usage](#usage)
5. [Support](#support)
6. [Contribution Guidelines](#contribution-guidelines)
7. [License](#license)
8. [Contributors](#contributors)
9. [Changelog](#)


## Requirements

1. Fountainpay version 1 API keys
2. Node version >= 6.9.x and npm >= 3.x.x
3. React version  >= 14


## Installation

Install the SDK

```bash
$ npm install Fountainpay-React-v1

# or
$ yarn add Fountainpay-React-v1

```


## Initialization

Import useFPCheckout to any component in your application and pass your config

```javascript
import { useFPCheckout } from 'Fountainpay-React-v1';
 const config = {
    key: 'FP-PUBK-**************************',
    tnx_ref: Date.now(),
    amount: 100,
    currency: 'NGN',
    channels: ["card", "qrcode", "directDebit"],
    customer: {
      email: 'user@gmail.com',
      phone_number: '070********',
      lastname: 'john',
      firstname:''
    },
    customizations: {
      title: 'my Payment Title',
      description: 'Payment for items in cart',
      logo: 'https://st2.depositphotos.com/4403291/7418/v/450/depositphotos_74189661-stock-illustration-online-shop-log.jpg',
    },
  };

 useFPCheckout(config)

```


## Usage

Add Fountainpayto your projects as a component or a react hook:

1. [As a Component](#components)
2. [Directly in your code](#hooks)
3. [Making recurrent payments](#recurring-payments)


### Components

```javascript
import React from 'react';
import { FPCheckoutButton, closePaymentModal } from 'Fountainpay-React-v1';

export default function App() {
  const config = {
    key: 'FP-PUBK-**************************',
    tnx_ref: Date.now(),
    amount: 100,
    currency: 'NGN',
    channels: ["card", "qrcode", "directDebit"],
    customer: {
      email: 'user@gmail.com',
      phone_number: '070********',
      lastname: 'john',
      firstname:''
    },
    customizations: {
      title: 'my Payment Title',
      description: 'Payment for items in cart',
      logo: 'https://st2.depositphotos.com/4403291/7418/v/450/depositphotos_74189661-stock-illustration-online-shop-log.jpg',
    },
  };


  const fwConfig = {
    ...config,
    text: 'Pay with Fountainpay!',
    callback: (response) => {
       console.log(response);
      closePaymentModal() // this will close the modal programmatically
    },
    onClose: () => {},
  };

  return (
    <div className="App">
     <h1>Hello Test user</h1>
      <FPCheckoutButton {...fwConfig} />
    </div>
  );
}
```


### Hooks

```javascript
import React from 'react';
import { useFPCheckout, closePaymentModal } from 'Fountainpay-React-v1';

export default function App() {
  const config = {
    key: 'FP-PUBK-**************************',
    tnx_ref: Date.now(),
    amount: 100,
    currency: 'NGN',
    channels: ["card", "qrcode", "directDebit"],
    customer: {
      email: 'user@gmail.com',
      phone_number: '070********',
      lastname: 'john',
      firstname:''
    },
    customizations: {
      title: 'my Payment Title',
      description: 'Payment for items in cart',
      logo: 'https://st2.depositphotos.com/4403291/7418/v/450/depositphotos_74189661-stock-illustration-online-shop-log.jpg',
    },
  };

  const handlePayment = useFPCheckout(config);

  return (
    <div className="App">
     <h1>Hello Test user</h1>

      <button
        onClick={() => {
          handlePayment({
            callback: (response) => {
               console.log(response);
                closePaymentModal() // this will close the modal programmatically
            },
            onClose: () => {},
          });
        }}
      >
        Payment with React hooks
      </button>
    </div>
  );
}
```


### Parameters

Read more about our parameters and how they can be used [here](https://doc.fountainpay.ng/docs/collecting-payments/inline).

| Parameter           | Always Required ? | Description                                                                                                                                                                                                                             |
| ------------------- | ----------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| key          | True              | Your API public key                                                                                                                                                                                                                     |
| tnx_ref              | True              | Your transaction reference. This MUST be unique for every transaction                                                                                                                                                                   |
| amount              | True              | Amount to charge the customer.                                                                                                                                                                                                          |
| currency            | False             | currency to charge in. Defaults to NGN                                                                                                                                                                                                  |
| integrity_hash      | False             | This is a sha256 hash of your FlutterwaveCheckout values, it is used for passing secured values to the payment gateway.                                                                                                                 |
| channels            | True              | This specifies the payment options to be displayed e.g - card, mobilemoney, ussd and so on.                                                                                                                                                                                                                                                         
| redirect_url        | False             | URL to redirect to when a transaction is completed. This is useful for 3DSecure payments so we can redirect your customer back to a custom page you want to show them.                                                                  |
| customer            | True              | This is an object that can contains your customer details: e.g - 'customer': {'email': 'example@example.com','phone_number': '080********', 'lastname': 'Richards', firstname:'Adedeji' }                                                                                        |
| metadata                | False             | This is an object that helps you include additional payment information to your request e.g {'consumer_id': 23,'consumer_mac': '92a3-912ba-1192a' }                                                                                     |
| customizations      | True              | This is an object that contains title, logo, and description you want to display on the modal e.g{'title': 'Pied Piper Payments','description': 'Middleout isn't free. Pay the price','logo': 'https://......' } |
| callback (function) | False             | This is the function that runs after payment is completed                                                                                                                                                                               |
| close (function)    | False             | This is the function that runs after payment modal is closed                                                                                                                                                                            |

## Other methods and descriptions:

Methods provided by the React SDK:

| Method Name  | Parameters  | Returns |Description |
| ------------- | ------------- | ------------- | ------------- |
| closePaymentModal  |  Null | Null | This methods allows you to close the payment modal via code. |

Please checkout [Fountainpay Documentation](https://docs.fountainpay.ng/docs/standard) for other available options you can add to the tag.



## Debugging Errors

We understand that you may run into some errors while integrating our library. You can read more about our error messages [here](https://docs.fountainpay.ng/docs/integration-guides/errors).

For `authorization` and `validation` error responses, double-check your API keys and request. If you get a `server` error, kindly engage the team for support.



# Support

For additional assistance using this library, please create an issue on the Github repo or contact the developer experience (DX) team via [email](mailto:developers@fountainpay.ng) or on [slack](https://bit.ly/34Vkzcg).

You can also follow us [@fountainpayng](https://twitter.com/fountainpayng) and let us know what you think 😊.



## Contribution Guidelines

We welcome contributions from the community. Read more about our community contribution guidelines [here](/CONTRIBUTING.md).


<a id="license"></a>

## License

By contributing to this library, you agree that your contributions will be licensed under its [MIT license](/LICENSE.md).

Copyright (c) Fountainpay Systems and Solutions.



## Contributors

- [Adedeji Richards](https://twitter.com/AbscentMan)
