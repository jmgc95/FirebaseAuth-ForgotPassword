<TextView
    android:id="@+id/forgotPasswordTextView"
    android:layout_width="wrap_content"
    android:layout_height="wrap_content"
    android:text="Forgot Password?"
    android:textColor="@color/linkColor"
    android:textStyle="bold"
    android:layout_marginTop="16dp"
    android:clickable="true"
    android:focusable="true"/>
    
// Add this line in the onCreate method after initializing other views
TextView forgotPasswordTextView = findViewById(R.id.forgotPasswordTextView);

// Set click listener for the "Forgot Password" TextView
forgotPasswordTextView.setOnClickListener(v -> {
    Intent intent = new Intent(LoginActivity.this, ForgotPasswordActivity.class);
    startActivity(intent);
});
 
 
 
package com.jmgcprojects.jmgctools;

import android.os.Bundle;
import android.widget.Button;
import android.widget.EditText;
import android.widget.Toast;

import androidx.appcompat.app.AppCompatActivity;
import com.google.firebase.auth.FirebaseAuth;

public class ForgotPasswordActivity extends AppCompatActivity {

    private EditText emailEditText;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_forgot_password);

        emailEditText = findViewById(R.id.emailEditText);
        Button resetPasswordButton = findViewById(R.id.resetPasswordButton);

        resetPasswordButton.setOnClickListener(v -> {
    String email = emailEditText.getText().toString().trim();
    if (email.isEmpty()) {
        Toast.makeText(this, "Please enter your email", Toast.LENGTH_SHORT).show();
    } else {
        // Send a password reset email using Firebase
        FirebaseAuth.getInstance().sendPasswordResetEmail(email)
            .addOnCompleteListener(task -> {
                if (task.isSuccessful()) {
                    Toast.makeText(this, "Password reset email sent to " + email, Toast.LENGTH_SHORT).show();
                    finish(); // Close the activity after sending the reset email
                } else {
                    Toast.makeText(this, "Failed to send reset email: " + task.getException().getMessage(), Toast.LENGTH_SHORT).show();
                }
            });
    }
});
    }
}



<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical"
    android:padding="16dp">

    <EditText
        android:id="@+id/emailEditText"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:hint="Enter your email"
        android:inputType="textEmailAddress"/>

    <Button
        android:id="@+id/resetPasswordButton"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:text="Reset Password"
        android:layout_marginTop="16dp"/>
</LinearLayout>


<activity android:name=".ForgotPasswordActivity"/>
