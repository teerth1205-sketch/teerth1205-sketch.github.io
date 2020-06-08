---
layout: post
title:      "ActiveStorage with some info on var, let and const!"
date:       2020-06-08 00:12:31 -0400
permalink:  activestorage_with_some_info_on_var_let_and_const
---

For my Rails API backend and javascript frontend project called snapstgram I used something that came with the rails 5.2 updatre called Active Storage. With it one can handle file uploads and store them. Once installed and executed after a rake task, it creates two tables that Active Storage needs,  **active_storage_attachments and active_storage_blobs**.  Here is what they do according to the frameworks readme: 

“Active Storage uses polymorphic associations via the Attachment join model, which then connects to the actual Blob. Blob models store attachment metadata (filename, content-type, etc.), and their identifier key in the storage service.”

All the previous methods for file upload required you to add columns in the exsisting model, where Active Storage doesnt. Active Storage also allows you to choose where to store your file, on your hardware or popular cloud providers. Amazon S3, Google Cloud Storage, and Microsoft Azure Storage are supported out of the box. 

**let, const and var:**

One of the features that came with ES6 is the addition of let and const, which can be used for variable declaration. The question is "what makes those different form var?"

var:

var declarations are globally scoped or function/locally scoped. The scope is global when a var variable is declared out of  a function. Meaning that any variable that is declared with var outside a function block is available for use in the whole window. Var is function scoped when it is declared wtihin a function meaning that it can only be accessed within that function. Var variables can be re-declared and updated. Also, Var variables are hoisted to the top of their scope and initialized with a value of undefined.

let: 

let is now preferred for variable declaration. let is block scoped, that is anything living insde of curly braces  { }. Trying to console.log() a let variable,  which is defined inside of a block, outside of that block will return an error. Just like var,  a variable declared with let can be updated within its scope. Unlike var, a let variable cannot be re-declared within its scope.Just like  var, let declarations are hoisted to the top. Unlike var which is initialized as undefined, the let keyword is not initialized. So if you try to use a let variable before declaration, you'll get a Reference Error.

const: 

Variables declared with the const maintain constant values. const declarations have some similarities with let declarations. Const declarations can only be accessed within the block they were declared, just like let. Const cannot be updated or re-declared, meaing that the value that the const was declared with will be the same value in it scope, and cannot be changed. Every const declaration mus t be initialized at the time of decleration. 
