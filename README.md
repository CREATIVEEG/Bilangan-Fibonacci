# Bilangan-Fibonacci-UTS

Nama           : Rhendy Diki Nugraha <br>
NIM            : 312210150 <br>
Kelas          : TI.22.A.1 <br>
Dosen Pengampu : Donny Maulana, S.Kom., M.M.S.I. <br>
Mata Kuliah : Pemrograman Mobile

## Daftar Isi
| Command | Description |
| --- | --- |
|  | List all new or modified files |
| git diff | Show file differences that haven't been staged |

## Pengantar
Assalamualaikum Wr. Wb <br>
Disini, Saya akan mengerjakan tugas dari pemrograman mobile. Yaitu, membuat sebuah aplikasi menampilkan bilangan fibonacci.<br>
Langsung saja, masuk ke tahap peng codingan.

### activity_fibonacci.xml
Pada layout ini, Saya membuat tiga buah button, dan satu textview. Button yang pertama, berfungsi sebagai tombol “Set Limit” yang nantinya ketika di tekan akan muncul sebuah pop-up untuk masukan limit angka yang ingin kita hitung. Button yang kedua, berfungsi sebagai tombol “count” yang nantinya ketika tombol ditekan akan menghitung bilangan fibonaccinya sesuai dengan yang kita limit. Button yang ketiga, berfungsi sebagai tombol Reset yang nantinya angka akan kembali ke awal.  Dan yang terakhir Textview, yang berfungsi untuk menampilkan angka atau bilangan fibonaccinya yang tepat berada di tengah.
Berikut ini coding lengkapnya :

```
<?xml version="1.0" encoding="utf-8"?>
<androidx.constraintlayout.widget.ConstraintLayout
    xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    tools:context=".MainActivity">

    <Button
        android:id="@+id/button_limit"
        android:layout_width="0dp"
        android:layout_height="wrap_content"
        android:layout_marginEnd="8dp"
        android:layout_marginStart="8dp"
        android:layout_marginTop="8dp"
        android:background="@color/colorPrimary"
        android:onClick="setLimit"
        android:textColor="@android:color/white"
        android:text="@string/enter_fibonacci_limit"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="parent"
        tools:ignore="UsingOnClickInXml,VisualLintButtonSize"/>


    <Button
        android:id="@+id/button_count"
        android:layout_width="190dp"
        android:layout_height="48dp"
        android:layout_marginStart="8dp"
        android:layout_marginEnd="8dp"
        android:layout_marginBottom="8dp"
        android:background="@color/colorPrimary"
        android:onClick="countUp"
        android:text="@string/button_label_count"
        android:textColor="@android:color/white"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintHorizontal_bias="0.0"
        app:layout_constraintStart_toStartOf="parent"
        tools:ignore="UsingOnClickInXml,VisualLintButtonSize" />

    <Button
        android:id="@+id/button_finish"
        android:layout_width="190dp"
        android:layout_height="48dp"
        android:layout_marginStart="8dp"
        android:layout_marginEnd="8dp"
        android:layout_marginBottom="8dp"
        android:background="@color/colorPrimary"
        android:onClick="back1"
        android:text="@string/button_label_finish"
        android:textColor="@android:color/white"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintHorizontal_bias="1.0"
        app:layout_constraintStart_toStartOf="parent"
        tools:ignore="UsingOnClickInXml" />

    <TextView
        android:id="@+id/show_count"
        android:layout_width="0dp"
        android:layout_height="0dp"
        android:layout_marginStart="8dp"
        android:layout_marginTop="8dp"
        android:layout_marginEnd="8dp"
        android:layout_marginBottom="8dp"
        android:background="#FFFF00"
        android:gravity="center_vertical"
        android:text="@string/count_initial_value"
        android:textAlignment="center"
        android:textColor="@color/colorPrimary"
        android:textSize="160sp"
        android:textStyle="bold"
        app:layout_constraintBottom_toTopOf="@id/button_count"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toBottomOf="@id/button_limit"
        tools:ignore="RtlCompat" />

</androidx.constraintlayout.widget.ConstraintLayout>
```
#### string.xml
```
<resources>
    <string name="app_name">Tugasenam</string>
    <string name="button_label_count">Count</string>
    <string name="count_initial_value"> </string>
    <string name="button_label_finish">Reset</string>
    <string name="enter_fibonacci_limit">Masukan Limit Angka</string>
</resources>
```
#### colors.xml
```
<?xml version="1.0" encoding="utf-8"?>
<resources>
    <color name="black">#FF000000</color>
    <color name="white">#FFFFFFFF</color>
    <color name="colorPrimary">#3F5185</color>
    <color name="colorPrimaryDark">#303F9F</color>
    <color name="colorAccent">#FF4081</color>
</resources>
```
### Tamplian Design
![Cuplikan layar 2023-10-31 132224](https://github.com/RhendyDikiN/Bilangan-Fibonacci/assets/115677376/60dd644a-ddfe-4f04-a074-83e234374158)

### MainActivity.java
Pada MainActivity.java berisi semua coding untuk fungsi-fungsinya. Seperti, fungsi untuk tombol-tombol, dan rumus bilangan fibonaccinya.
```
package com.example.tugastujuh;

import android.app.AlertDialog;
import android.content.DialogInterface;
import android.os.Bundle;
import android.view.View;
import android.widget.EditText;
import android.widget.TextView;
import androidx.appcompat.app.AppCompatActivity;

public class MainActivity extends AppCompatActivity {
    private TextView showCount;
    private int count = 1;
    private long fibNMinus1 = 1;
    private long fibNMinus2 = 0;
    private int limit = -1; // Inisialisasi limit dengan nilai default

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_fibonacci);

        showCount = findViewById(R.id.show_count);
    }

    public void countUp(View view) {
        if (count == 0) {
            showCount.setText("0");
        } else if (count == 1) {
            showCount.setText("1");
        } else {
            if (limit != -1 && count > limit) {
                // Jika count melebihi limit, atur ulang perhitungan
                count = 0;
                fibNMinus1 = 1;
                fibNMinus2 = 0;
                showCount.setText(getString(R.string.count_initial_value));
            } else {
                long fibCurrent = fibNMinus1 + fibNMinus2;
                fibNMinus2 = fibNMinus1;
                fibNMinus1 = fibCurrent;
                showCount.setText(String.valueOf(fibCurrent));
            }
        }

        count++;
    }

    public void back1(View view) {
        count = 1;
        fibNMinus1 = 1;
        fibNMinus2 = 0;
        showCount.setText(getString(R.string.count_initial_value));
    }

    public void setLimit(View view) {
        // Create and display a dialog to set the limit
        AlertDialog.Builder builder = new AlertDialog.Builder(this);
        builder.setTitle("Set Limit");

        final EditText input = new EditText(this);
        input.setInputType(android.text.InputType.TYPE_CLASS_NUMBER);
        builder.setView(input);

        builder.setPositiveButton("OK", new DialogInterface.OnClickListener() {
            @Override
            public void onClick(DialogInterface dialog, int which) {
                // Get the limit from the input and set it for calculations
                String limitStr = input.getText().toString();
                limit = Integer.parseInt(limitStr);
            }
        });

        builder.setNegativeButton("Cancel", new DialogInterface.OnClickListener() {
            @Override
            public void onClick(DialogInterface dialog, int which) {
                dialog.cancel();
            }
        });

        builder.show();
    }
}
```
### Hasil RUN
https://github.com/RhendyDikiN/Bilangan-Fibonacci/assets/115677376/cdf9bb57-c8a2-4857-a4a0-a1fac6838cba

