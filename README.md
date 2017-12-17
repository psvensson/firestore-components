# \<firestore-components\>

Very simple Polymer Web Components for accessing the Google Cloud Firestore database

## Prerequisites

These components assume that they live in a web-page where firestore has been loaded already, with something like this in the index.html;

    <script defer src="/__/firebase/4.6.0/firebase-app.js"></script>
    <script defer src="/__/firebase/4.6.0/firebase-auth.js"></script>
    <script defer src="/__/firebase/4.6.0/firebase-messaging.js"></script>
    <script defer src="/__/firebase/4.6.0/firebase-firestore.js"></script>
    <script defer src="/__/firebase/4.6.0/firebase-storage.js"></script>

What I did was to generate a sample app using the firebase CLI, and then copy-pasted Polymer init stuff from another project.

## firestore-path

<firestore-path id="pathref" data="{{channel}}" doc="{{channeldoc}}" path="channels/{{channelid}}"></firestore-path>

Firestore-path gets one specific document from your Firestore database. By changing the 'path'parameter, you change which document is fecthed. The data fo the document (as you would get using doc.data()) is set to the 'data' parameter. If you need to access the raw doc reference, that is accessible through the 'doc' parameter.

To update or delete the reference document from your code, use this.shadowRoot.querySelector('#pathref').setDoc() or this.shadowRoot.querySelector('#pathref').deleteDoc().

When the document referenced gets an update, it will propagate out to this element, which will also trigger to change 'data' and 'doc' proeprties reactively.

## firestore-all

<firestore-all type="mythings" list="{{allthings}}"></firestore-all>

This will get all documents in a collection named in the 'type' proeprty, loop through the references and put the data properties as object in an array accessible in the 'list' property. It can be quite a bit of stuff, but can be usefull in the beginning when debugging.

## firestore-list

<firestore-list type="mythings" references="{{refs}}" list="{{listofthings}}"></firestore-list>

Frequently you have stored an array of references on a document, which points to other documents, like an array of movies a user has seen, or somethings like that. List od doc.data()'d things will in the 'list' property.

## firestore-query

<firestore-query type="mythings" property="city" operation="==" value="{{comparecity}}"></firestore-query>

Will query you collection using the same logic as foudn in the doucmentation here; https://firebase.google.com/docs/reference/js/firebase.firestore.Query

## firestore-subcollection

<firestore-subcollection doc="{{mydoc}}" path="subthings" list={{listofsubthings}}"></firestore-sunbcollection>

Will do the same as firestore-all, but for a subcollections of documents under another docuiment. Here you can use the 'doc' property on firestore-path to provide input.

