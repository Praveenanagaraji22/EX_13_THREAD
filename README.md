# EX_13_THREAD
# Date: 07.11.2024
## AIM:
To develop a thread synchronization concept with the help of clicking the button in Android Studio.
## EQUIPMENTS REQUIRED:
Latest Version Android Studio
## ALGORITHM:
Step 1: Open Android Studio and then click on File -> New -> New project.
Step 2: Then type the Application name as HelloWorld and click Next.
Step 3: Then select the Minimum SDK as shown below and click Next.
Step 4: Then select the Empty Activity and click Next. Finally click Finish.
Step 5: Design layout in activity_main.xml.
Step 6: Display message give in MainActivity file.
Step 7: Save and run the application.
## PROGRAM:
```
Program to print the text “optionmenu”.
Developed by: PRAVEENA N
Registeration Number : 212222040122
```
mainActivity.java
```
package com.example.exp13;
import androidx.appcompat.app.AppCompatActivity;
import android.os.Bundle;
import android.os.Bundle;
import android.os.Handler;
import android.util.Log;
import android.view.View;
import android.widget.TextView;
import androidx.appcompat.app.AppCompatActivity;
import java.util.concurrent.Semaphore;
public class MainActivity extends AppCompatActivity {
    private static final String TAG = "MainActivity";
    private static final Object lock = new Object();
    private static final int MAX_THREADS = 5;
    private static final Semaphore semaphore = new Semaphore(MAX_THREADS);
    private int counter = 0;
    private TextView textView;
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
        textView = findViewById(R.id.text_view);}
    public void incrementCounter(View view) {
        new Thread(() -> {
            try {
                semaphore.acquire();
                synchronized (lock) {
                    counter++;}
            } catch (InterruptedException e) {
                // Log an error if the thread is interrupted
                Log.e(TAG, "Thread interrupted", e);
            } finally {
                semaphore.release(); }
            updateTextView();
        }).start(); }
    private void updateTextView() {
        new Handler(getMainLooper()).post(() -> textView.setText(String.valueOf(counter)));
    }}
```
activity_main.xml
```
<?xml version="1.0" encoding="utf-8"?>
<androidx.constraintlayout.widget.ConstraintLayout
    xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    tools:context=".MainActivity">
    <!-- A text view to display the count -->
    <TextView
        android:id="@+id/text_view"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="0"
        android:textSize="32sp"
        app:layout_constraintBottom_toTopOf="@+id/increment_button"
        app:layout_constraintLeft_toLeftOf="parent"
        app:layout_constraintRight_toRightOf="parent"
        app:layout_constraintTop_toTopOf="parent" />
    <!-- A button to increment the count -->
    <Button
        android:id="@+id/increment_button"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:onClick="incrementCounter"
        android:text="Increment"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintLeft_toLeftOf="parent"
        app:layout_constraintRight_toRightOf="parent"
        app:layout_constraintTop_toTopOf="parent" />
</androidx.constraintlayout.widget.ConstraintLayout>
```
## OUTPUT
![384413860-8959ab62-39b5-4d81-b029-200b2f5ab089](https://github.com/user-attachments/assets/fe936ff8-f981-484b-83b7-6a6a1275df91)
## RESULT
The application is successfully displayed for thread synchronization concept with the help of clicking the button in Android Studio.
