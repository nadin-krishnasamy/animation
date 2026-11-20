# Ex.No: 11 Develop a application to add animations to ImageView,Move,blink,fade,clockwise,zoom,slide operations are perform in android studio.


## AIM:

To develop a application to add animation to imageview,move,blink,fade,clockwise,zoom,slide operation using Android Studio.

## EQUIPMENTS REQUIRED:

Android Studio(Latest Version)

## ALGORITHM:
1.Start the Android application and set activity_main.xml as the main layout.

2.Design the UI in activity_main.xml with an ImageView and buttons for Blink, Rotate, Fade, Move, Slide, Zoom, and Stop.

3.Create individual animation XML files (blink.xml, rotate.xml, fade.xml, move.xml, slide.xml, zoom.xml) inside the res/anim/ directory.

4.Initialize the ImageView and Button components in MainActivity.java using findViewById().

5.Attach OnClickListener events to each animation button to load its corresponding XML resource via AnimationUtils.loadAnimation().

6.Execute the selected animation on the ImageView using imageView.startAnimation(), and clear it on the Stop button click via imageView.clearAnimation().

7.Stop the execution when the user exits the application.


## PROGRAM:
```
/*
Program to display animation operation”.
Developed by: NADIN KRISHNASAMY B
Registeration Number : 212225240095
*/
```
### activity_main.xml
```
<?xml version="1.0" encoding="utf-8"?>
<androidx.constraintlayout.widget.ConstraintLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:id="@+id/main"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    tools:context=".MainActivity">

    <ImageView
        android:id="@+id/imageView"
        android:layout_width="200dp"
        android:layout_height="200dp"
        android:layout_marginBottom="61dp"
        app:layout_constraintBottom_toTopOf="@+id/fade"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintStart_toStartOf="parent"
        app:srcCompat="@drawable/img" />

    <TextView
        android:id="@+id/textView"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="EX - 06 ANIMATION"
        android:textColor="#000000"
        android:textSize="20sp"
        android:textStyle="bold"
        app:layout_constraintBottom_toTopOf="@+id/imageView"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="parent" />

    <Button
        android:id="@+id/blink"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_marginBottom="28dp"
        android:backgroundTint="#000000"
        android:text="BLINK"
        app:layout_constraintBottom_toTopOf="@+id/move"
        app:layout_constraintEnd_toStartOf="@+id/rotate"
        app:layout_constraintStart_toStartOf="parent" />

    <Button
        android:id="@+id/rotate"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_marginTop="60dp"
        android:layout_marginEnd="31dp"
        android:backgroundTint="#000000"
        android:text="ROTATE"
        app:layout_constraintEnd_toStartOf="@+id/zoom"
        app:layout_constraintTop_toBottomOf="@+id/imageView" />

    <Button
        android:id="@+id/fade"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_marginBottom="325dp"
        android:backgroundTint="#000000"
        android:text="FADE"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintStart_toEndOf="@+id/rotate" />

    <Button
        android:id="@+id/move"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_marginStart="32dp"
        android:backgroundTint="#000000"
        android:text="MOVE"
        app:layout_constraintBaseline_toBaselineOf="@+id/slide"
        app:layout_constraintStart_toStartOf="parent" />

    <Button
        android:id="@+id/zoom"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_marginEnd="32dp"
        android:backgroundTint="#000000"
        android:text="ZOOM"
        app:layout_constraintBaseline_toBaselineOf="@+id/slide"
        app:layout_constraintEnd_toEndOf="parent" />

    <Button
        android:id="@+id/slide"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_marginTop="30dp"
        android:backgroundTint="#000000"
        android:text="SLIDE"
        app:layout_constraintEnd_toStartOf="@+id/zoom"
        app:layout_constraintHorizontal_bias="0.493"
        app:layout_constraintStart_toEndOf="@+id/move"
        app:layout_constraintTop_toBottomOf="@+id/rotate" />

    <Button
        android:id="@+id/stop"
        android:layout_width="167dp"
        android:layout_height="68dp"
        android:backgroundTint="#F03535"
        android:text="STOP ANIMATION"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toBottomOf="@+id/slide" />
</androidx.constraintlayout.widget.ConstraintLayout>
```
### MainActivity.java
```
package com.example.ex_06animation;

import android.os.Bundle;
import android.view.View;
import android.view.animation.Animation;
import android.view.animation.AnimationUtils;
import android.widget.Button;
import android.widget.ImageView;

import androidx.appcompat.app.AppCompatActivity;

import com.example.ex_06animation.R;

public class MainActivity extends AppCompatActivity {

    private ImageView imageView;
    private Button blink, rotate, fade, move, slide, zoom, stop;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        imageView = findViewById(R.id.imageView);
        blink = findViewById(R.id.blink);
        rotate = findViewById(R.id.rotate);
        fade = findViewById(R.id.fade);
        move = findViewById(R.id.move);
        slide = findViewById(R.id.slide);
        zoom = findViewById(R.id.zoom);
        stop = findViewById(R.id.stop);

        createAnimation(blink, R.anim.blink);
        createAnimation(rotate, R.anim.rotate);
        createAnimation(fade, R.anim.fade);
        createAnimation(move, R.anim.move);
        createAnimation(slide, R.anim.slide);
        createAnimation(zoom, R.anim.zoom);

        stop.setOnClickListener(v -> imageView.clearAnimation());
    }

    private void createAnimation(View view, int animResId) {
        view.setOnClickListener(v -> {
            Animation animation = AnimationUtils.loadAnimation(MainActivity.this, animResId);
            imageView.startAnimation(animation);
        });
    }
}
```
### blink.xml
```
<?xml version="1.0" encoding="utf-8"?>
<set xmlns:android="http://schemas.android.com/apk/res/android">
    <alpha
        android:duration="500"
        android:fromAlpha="0.0"
        android:interpolator="@android:anim/accelerate_interpolator"
        android:repeatCount="infinite"
        android:repeatMode="reverse"
        android:toAlpha="1.0" />
</set>
```
### rotate.xml
```
<?xml version="1.0" encoding="utf-8"?>
<set xmlns:android="http://schemas.android.com/apk/res/android">
    <rotate
        android:duration="1000"
        android:fromDegrees="0"
        android:pivotX="50%"
        android:pivotY="50%"
        android:repeatCount="infinite"
        android:toDegrees="360" />
</set>
```
### fade.xml
```
<?xml version="1.0" encoding="utf-8"?>
<set xmlns:android="http://schemas.android.com/apk/res/android">
    <alpha
        android:duration="1200"
        android:fromAlpha="0.0"
        android:interpolator="@android:anim/accelerate_decelerate_interpolator"
        android:toAlpha="1.0" />
</set>
```
### move.xml
```
<?xml version="1.0" encoding="utf-8"?>
<set xmlns:android="http://schemas.android.com/apk/res/android">
    <translate
        android:duration="1000"
        android:fromXDelta="0%"
        android:repeatCount="infinite"
        android:repeatMode="reverse"
        android:toXDelta="30%" />
</set>
```
### slide.xml
```
<?xml version="1.0" encoding="utf-8"?>
<set xmlns:android="http://schemas.android.com/apk/res/android">
    <translate
        android:duration="1000"
        android:fromXDelta="0%p"
        android:interpolator="@android:anim/accelerate_decelerate_interpolator"
        android:repeatCount="infinite"
        android:repeatMode="reverse"
        android:toXDelta="50%p" />
</set>
```
## OUTPUT
  
<img width="1917" height="1078" alt="Screenshot 2026-11-19 105202" src="https://github.com/user-attachments/assets/3addc852-4787-479a-a409-b61fd942e9ae" />
<img width="1917" height="1078" alt="Screenshot 2026-11-20 184417" src="https://github.com/user-attachments/assets/797a424c-4782-41bc-8b47-7fc96cb7cd71" />
<img width="1917" height="1078" alt="Screenshot 2026-11-20 184435" src="https://github.com/user-attachments/assets/1728934b-3d15-475e-8951-69b1b6008a83" />
<img width="1917" height="1078" alt="Screenshot 2026-11-20 184516" src="https://github.com/user-attachments/assets/469181fa-7eee-4fec-a5ca-e6d798221f79" />
<img width="1917" height="1078" alt="Screenshot 2026-11-20 184540" src="https://github.com/user-attachments/assets/276a40d7-97d0-4478-90fb-e7dea74a7779" />



## RESULT
