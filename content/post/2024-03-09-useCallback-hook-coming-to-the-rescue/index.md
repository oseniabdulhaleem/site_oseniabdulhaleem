---
title: "Date seems to be affecting hugo"
subtitle: ""
description: ""
date: 2024-03-06
author:      ""
image: ""
tags: ["tech", "software"]
categories: ["Tech", "software"]
---

/**************\*\***************/

/**************\*\***************/

/**************\*\***************/

/** ARTICLE SOONNNNNNNNNN **/

/**************\*\***************/

/**************\*\***************/

/**************\*\***************/



I was recently faced with a challenge to update a button payment reference on success and failure and this was how react useCallback hook came to the rescue

// import { PaystackConsumer } from 'react-paystack';

// export default function PaystackButton() {
// // Generate initial config with a function to ensure dynamic reference updates.
// const config = { amount: 1000 };
// const getUpdatedConfig = () => ({
// email: 'love@.com',
// amount: config.amount, // Amount is in the country's lowest currency. E.g Kobo, so 20000 kobo = N200
// publicKey: 'pk*test*',
// reference: new Date().getTime().toString(), // Generate a new reference on each call
// metadata: {
// custom_fields: [
// {
// group_name: 'ATM MOVIES',
// },
// // To pass extra metadata, add an object with the same fields as above
// ],
// },
// });

// const handleSuccess = (reference) => {
// console.log(reference);
// };

// const handleClose = () => {
// console.log('closed');
// };

// return (
// <PaystackConsumer
// {...getUpdatedConfig()}
// text="Pay Now"
// onSuccess={handleSuccess}
// onClose={handleClose}
// >
// {({ initializePayment }) => (
// <button
// type="button"
// onClick={() => initializePayment(getUpdatedConfig(), handleSuccess, handleClose)}
// >
// Pay {config.amount / 100}
// </button>
// )}
// </PaystackConsumer>
// );
// }

import React, { useState, useCallback } from 'react';
import { PaystackConsumer } from 'react-paystack';

export default function PaystackButton() {
const [key, setKey] = useState(0); // Add a key state to force re-render
const config = { amount: 1000 };

const getUpdatedConfig = useCallback(
() => ({
email: 'lol my email',
amount: config.amount, // Amount is in the country's lowest currency. E.g Kobo, so 20000 kobo = N200
publicKey: 'lol my key',
reference: `${new Date().getTime()}`, // Generate a new reference on each call
metadata: {
custom_fields: [
{
group_name: 'ATM MOVIES',
},
// To pass extra metadata, add an object with the same fields as above
],
},
}),
[key]
); // Add key as a dependency to update config when key changes

const handleSuccess = useCallback((reference) => {
console.log(reference);
setKey((prevKey) => prevKey + 1); // Update key to force re-render on success
}, []);

const handleClose = useCallback(() => {
console.log('closed');
setKey((prevKey) => prevKey + 1); // Update key to force re-render on close
}, []);

return (
<PaystackConsumer
{...getUpdatedConfig()}
text="Pay Now"
onSuccess={handleSuccess}
onClose={handleClose} >
{({ initializePayment }) => (
<button
key={key} // Use key here to force re-render the button as well
type="button"key
onClick={() => initializePayment(getUpdatedConfig(), handleSuccess, handleClose)} >
Pay {config.amount / 100}
</button>
)}
</PaystackConsumer>
);
}
