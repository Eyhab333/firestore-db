

## Add data to Firestore

``` 
import { doc, setDoc } from "firebase/firestore"; 

await setDoc(doc(db, "Ali Hassan", "test123"), {
  userName: "Ali Hassan",
  age: 28,
  married: false,
  websites: ["c4a.dev", "courses4arab.com"]
}); 
```

## Get data From Firestore as array

```
Npm I React-Firebase-Hooks
```

### Get all documents

```
 import { useCollection } from "react-firebase-hooks/firestore";
 import { collection } from "firebase/firestore";

 const [value, loading, error] = useCollection(collection(db, COLLECTION NAME));


 // explain 
 value.docs >>> ARRAY >>> array of documents
 value.docs.map(***)
```

### Get all documents in specific order

```
import { useCollection } from "react-firebase-hooks/firestore";
import { collection, orderBy, query, limit } from "firebase/firestore";

const [value, loading, error] = useCollection(
  query(collection(db, user.uid), orderBy("id"))
);

// get first 3 documents
const [value, loading, error] = useCollection(
  query(collection(db, user.uid), orderBy("id"), limit(3))
);

// Get the data in reverse order
const [value, loading, error] = useCollection(
  query(collection(db, user.uid), orderBy("id", "desc"))
);
```

### get a specific group of documents

```
import { useCollection } from "react-firebase-hooks/firestore";
import { collection, query, where } from "firebase/firestore";

const [value, loading, error] = useCollection(
  query(collection(db, user.uid), where("completed", "==", true))
);
```
Invalid: Range filter and first orderBy on different fields

### get one document

```
import { useDocument } from "react-firebase-hooks/firestore";
import { doc } from "firebase/firestore";

 const [value, loading, error] = useDocument(doc(db, user.uid, id));

 // explain 
 value.data() >>> OBJECT
 value.data().***
 ```

## Update data in Firestore
- Update a document

```
import { doc, updateDoc } from "firebase/firestore";

await updateDoc(doc(db, user.uid, id), {
  title: eo.target.value,
});
```

- Update an array
```
// Add element to an array
import { arrayUnion, doc, updateDoc } from "firebase/firestore";
 
await updateDoc(doc(db, user.uid, id), {
  details: arrayUnion(VARIABLE),
});
```

```
// Remove element from an array
import { arrayRemove, doc, updateDoc } from "firebase/firestore";
 
await updateDoc(doc(db, user.uid, id), {
   details: arrayRemove(ITEM),
});
```

## Delete data from Firestore

- Delete a document from Firestore
```
import { doc, updateDoc } from "firebase/firestore";

await deleteDoc(doc(db, user.uid, id));
```

- Delete specific fields from a document
```
import { doc, updateDoc, deleteField } from "firebase/firestore";

await updateDoc(doc(db, user.uid, id), {
     title: deleteField()
  });
```