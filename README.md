# TableLayout
Simple app to add rows dynamically. 


activity_main.xml

<?xml version="1.0" encoding="utf-8"?>
    <LinearLayout
        xmlns:android="http://schemas.android.com/apk/res/android"
        android:layout_width="fill_parent"
        android:layout_height="fill_parent"
        android:orientation="vertical">

        <Button
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:id="@+id/Button01"
            android:text="@string/text_string"/>
        <Button
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:id="@+id/Button02"
            android:text="@string/text_string2"/>

    <ScrollView
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:id="@+id/ScrollView01">

            <TableLayout
                android:layout_width="fill_parent"
                android:layout_height="wrap_content"
                android:id="@+id/TableLayout01"
                android:stretchColumns="0">

                <TableRow
                    android:layout_width="wrap_content"
                    android:layout_height="wrap_content"
                    android:id="@+id/TableRow01">

                    <TextView
                        android:layout_width="fill_parent"
                        android:layout_height="wrap_content"
                        android:id="@+id/TextView01"
                        android:text="@string/textfield"/>


                    <DigitalClock
                        android:layout_width="wrap_content"
                        android:layout_height="wrap_content"
                        android:id="@+id/digitalClock01"
                        android:text="@string/digital"/>

                    <CheckBox
                        android:layout_width="wrap_content"
                        android:layout_height="wrap_content"
                        android:id="@+id/CheckBox01"
                        android:text=""/>
                </TableRow>
            </TableLayout>
    </ScrollView>
    </LinearLayout>


MainActivity.java
package com.example.elii.tablelayout;

import android.app.Activity;
import android.os.Bundle;
import android.view.View;
import android.view.View.OnClickListener;
import android.widget.Button;
import android.widget.CheckBox;
import android.widget.DigitalClock;
import android.widget.LinearLayout;
import android.widget.TableLayout;
import android.widget.TableRow;
import android.widget.TextView;
import android.widget.LinearLayout.LayoutParams;




public class MainActivity extends Activity implements OnClickListener {
    /**
     * Called when the activity is first called.
     */

    Button btn;
    Button remove_btn;
    int counter = 0;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
        btn = (Button) findViewById(R.id.Button01);
        btn.setOnClickListener(this);
        remove_btn = (Button) findViewById(R.id.Button02);
        remove_btn.setOnClickListener(this);
    }

    public void onClick(View view) {
        TableLayout tl = (TableLayout) findViewById(R.id.TableLayout01);
        switch(view.getId()) {
            case R.id.Button01:

            TableRow tr = new TableRow(this);
            counter++;
            TextView tv = new TextView(this);
            tv.setText("text" + counter);
            CheckBox cb = new CheckBox(this);
            DigitalClock dc = new DigitalClock(this);
            tr.addView(tv);
            tr.addView(dc);
            tr.addView(cb);
            tl.addView(tr, new TableLayout.LayoutParams(LayoutParams.WRAP_CONTENT,LayoutParams.WRAP_CONTENT));
                break;
            case R.id.Button02:
               int childCount = tl.getChildCount();
             //tl=(TableLayout)findViewById(R.id.TableLayout01);
                for (int i=0; i<childCount; i++) {
                   CheckBox checkBox = ((CheckBox)((TableRow)tl.getChildAt(i)).getChildAt(2));
                    boolean isChecked = checkBox.isChecked();
                   // TableRow currentRow = (TableRow)tl.getChildAt(i);
                  // CheckBox checkBox = (CheckBox)currentRow.getChildAt(2);
                    if(isChecked){
                        tl.removeView(checkBox);
                    }

                }

                break;
        }


    }
}
