package com.ionicbyte.pidigits;

import android.annotation.TargetApi;
import android.app.AlertDialog;
import android.content.Context;
import android.content.DialogInterface;
import android.os.Bundle;
import android.support.v7.app.ActionBarActivity;
import android.view.View;
import android.widget.Button;
import android.widget.EditText;
import android.widget.TextView;
import android.widget.Toast;

public class Main extends ActionBarActivity {

    Button button;
    EditText editView;
    TextView textView, textView2;
    long startTime, elapsedTime;
    double elapsedSec;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.main);
        button = (Button) findViewById(R.id.button1);
        editView = (EditText) findViewById(R.id.editText1);
        textView = (TextView) findViewById(R.id.textView1);
        textView2 = (TextView) findViewById(R.id.textView2);

        textView.setOnLongClickListener(new View.OnLongClickListener() {
            @Override
            public boolean onLongClick(View view) {
                AlertDialog.Builder builder = new AlertDialog.Builder(Main.this);
                builder.setItems(R.array.array,
                        new DialogInterface.OnClickListener() {
                            public void onClick(DialogInterface dialog, int item) {
                                dialog.dismiss();
                                copyClipboard(textView.getText().toString());
                            }
                        });
                AlertDialog alert = builder.create();
                alert.show();
                return false;
            }
        });
        button.setOnClickListener(new View.OnClickListener() {

            @Override
            public void onClick(View arg0) {
                calculatePi();
            }
        });
    }

    public void calculatePi() {
        startTime = System.nanoTime();

        textView.setText(Pi.pi(Integer.parseInt(editView.getText().toString()))
                .toString());

        elapsedTime = System.nanoTime() - startTime;
        elapsedSec = (double) elapsedTime / 1000000000;
        textView2.setText(getString(R.string.time) + " " + String.valueOf(elapsedSec) + " s");
    }

    @SuppressWarnings("deprecation")
    @TargetApi(11)
    public void copyClipboard(String text) {
        int sdk = android.os.Build.VERSION.SDK_INT;

        if (sdk < android.os.Build.VERSION_CODES.HONEYCOMB) {
            android.text.ClipboardManager clipboard = (android.text.ClipboardManager) getSystemService(Context.CLIPBOARD_SERVICE);
            clipboard.setText(text);
        } else {
            android.content.ClipboardManager clipboard = (android.content.ClipboardManager) getSystemService(Context.CLIPBOARD_SERVICE);
            android.content.ClipData clip = android.content.ClipData
                    .newPlainText("Pi", text);
            clipboard.setPrimaryClip(clip);
        }
        Toast.makeText(getApplicationContext(),
                Main.this.getString(R.string.copy), Toast.LENGTH_LONG).show();
    }
}