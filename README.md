# Ex.No:2 Create a simple application client and server service using AIDL interface in android studio.


## AIM:

To create a AIDL interface and communicate the process between client and server using AIDL interface in Android Studio.

## EQUIPMENTS REQUIRED:

Android Studio(Min.required Artic Fox)

## ALGORITHM:

Step 1: Open Android Stdio and then click on File -> New -> New project.

Step 2: Then type the Application name as CSAIDL and click Next. 

Step 3: Then select the Minimum SDK as shown below and click Next.

Step 4: Then select the Empty Activity and click Next. Finally click Finish.

Step 5: Design layout in activity_main.xml.

Step 6: Display message give in MainActivity file(client/server).

Step 7: Save and run the application.

## PROGRAM:
```
Program to print the client/server services using AIDL”.
Developed by:D.Amarnath Reddy
Registeration Number :2122212400512
```
## MainActivity.java:
~~~
package com.example.aidlapp88;

import androidx.appcompat.app.AppCompatActivity;

import android.content.ComponentName;
import android.content.Context;
import android.content.Intent;
import android.content.ServiceConnection;
import android.os.Bundle;
import android.os.IBinder;
import android.os.RemoteException;
import android.view.View;
import android.widget.Button;
import android.widget.EditText;
import android.widget.TextView;

public class MainActivity extends AppCompatActivity implements View.OnClickListener {
    EditText editFirstNumber,editSecondnumber;
    Button btnMultiply;
    TextView txtResult;
    MultiplyInterface myInterface;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        editFirstNumber = (EditText) findViewById(R.id.editFirstNumber);
        editSecondnumber = (EditText) findViewById(R.id.editSecondNumber);
        btnMultiply = (Button) findViewById(R.id.btnMultiply);
        txtResult = (TextView) findViewById(R.id.txtResult);

        btnMultiply.setOnClickListener(MainActivity.this);

        Intent multiplyService = new Intent(MainActivity.this, MultiplicationService.class);

        bindService(multiplyService, myServiceConnection, Context.BIND_AUTO_CREATE);
    }

        ServiceConnection myServiceConnection = new ServiceConnection() {
            @Override
            public void onServiceConnected(ComponentName componentName, IBinder iBinder) {

                myInterface = MultiplyInterface.Stub.asInterface(iBinder);

            }
                @Override
                        public void onServiceDisconnected(ComponentName componentName)
                {

                }



            };
    @Override
    public void onClick(View v) {

        int firstNumber = Integer.parseInt(editFirstNumber.getText().toString());
        int secondNumber = Integer.parseInt(editSecondnumber.getText().toString());

        try{
            int result = myInterface.multiplyTwoValuesTogether(firstNumber,secondNumber);
            txtResult.setText(result + "");

        }catch(RemoteException e){
            e.printStackTrace();
        }

    }
}
~~~
## Activity_main.xml:
~~~

<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical"
    tools:context=".MainActivity">


    <EditText
        android:id="@+id/editFirstNumber"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:ems="10"
        android:inputType="number" />

    <EditText
        android:id="@+id/editSecondNumber"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:ems="10"
        android:inputType="number" />

    <Button
        android:id="@+id/btnMultiply"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:text="Multiply" />

    <TextView
        android:id="@+id/txtResult"
        android:layout_width="match_parent"
        android:layout_height="49dp"
        android:text="textview" />

</LinearLayout>
~~~
## MultiplyInterrface.aidl:
~~~
// MultiplyInterface.aidl
package com.example.aidlapp88;

// Declare any non-default types here with import statements

interface MultiplyInterface {

     int multiplyTwoValuesTogether(int firstnumber, int secondnumber);
}
~~~
## MultiplicationService.java:
~~~
package com.example.aidlapp88;

import android.app.Service;
import android.content.Intent;
import android.os.IBinder;
import android.os.RemoteException;

public class MultiplicationService extends Service {
    public MultiplicationService() {
    }

    @Override
    public IBinder onBind(Intent intent) {
        return myBinder;

    }
    MultiplyInterface.Stub myBinder = new MultiplyInterface.Stub() {
        @Override
        public int multiplyTwoValuesTogether(int firstnumber, int secondnumber)
                throws RemoteException {
           return firstnumber * secondnumber;
        }
    };
}
~~~
## OUTPUT
![image](https://user-images.githubusercontent.com/93427224/236429579-68b9c043-2d55-473a-8616-78b6cac206a4.png)

![image](https://user-images.githubusercontent.com/93427224/236429619-2ab1c211-3bb2-4f88-bedf-f049dedf9a3e.png)

## RESULT
Thus a Simple Android Application to create a AIDL interface and communicate the process between client and server using AIDL interface in Android Studio is developed and executed successfully.
