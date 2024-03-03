# Title
Mobile Application
## Context
The decision to utilize Firebase as the backend solution for our mobile application development project.

1. Scalability and Performance Concerns:

Current solution: Existing backend infrastructure struggles to handle increasing user base and data volume, leading to slow loading times and performance issues.

2. Cost Optimization:

Challenge: The current backend solution incurs high maintenance and operational costs.

## Decision
After careful consideration, we have chosen to leverage Firebase for its range of services that fulfill the important demands to develop mobile application, such as Realtime Database, Authentication, Cloud Firestore, Cloud Storage, and Hosting.


## Rationale
Firebase offer lots of tools and solution for complete backend service in their own. It's provide scalability in later. developer can start without cost and can extended their own budget later.

## Consequences
Pros – What becomes easier?
Cons – What becomes more difficult?

## Sample code
Give some sample code related to this decision.
// Add Firebase Authentication and Firestore dependencies to your app build.gradle file

// Firebase Authentication
implementation 'com.google.firebase:firebase-auth-ktx:20.0.4'

// Cloud Firestore
implementation 'com.google.firebase:firebase-firestore-ktx:23.0.2'

// Import necessary Firebase modules in your Kotlin file
import com.google.firebase.auth.FirebaseAuth
import com.google.firebase.firestore.FirebaseFirestore

// Initialize Firebase services in your application
val auth: FirebaseAuth = FirebaseAuth.getInstance()
val db: FirebaseFirestore = FirebaseFirestore.getInstance()

// Sign up user with email and password
auth.createUserWithEmailAndPassword(email, password)
    .addOnCompleteListener(this) { task ->
        if (task.isSuccessful) {
            // Sign up successful, save user data to Firestore
            val user = hashMapOf(
                "email" to email,
                // Add more user data fields as needed
            )
            db.collection("users").document(auth.currentUser?.uid ?: "")
                .set(user)
                .addOnSuccessListener {
                    // User data saved successfully
                }
                .addOnFailureListener { e ->
                    // Error saving user data
                }
        } else {
            // Sign up failed
        }
    }

// Sign in user with email and password
auth.signInWithEmailAndPassword(email, password)
    .addOnCompleteListener(this) { task ->
        if (task.isSuccessful) {
            // Sign in successful
        } else {
            // Sign in failed
        }
    }

// Sign out user
auth.signOut()

// Listen for authentication state changes
auth.addAuthStateListener { firebaseAuth ->
    val user = firebaseAuth.currentUser
    if (user != null) {
        // User is signed in
    } else {
        // User is signed out
    }
}
