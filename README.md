# Лабораторная работа №3. Работа с базой данных.
Выполнила: Усова Валентина, ИСП-221С
## Что делает приложение?

Приложение будет взаимодействовать с базой данных, создавать и управлять таблицей “Одногруппники”.

## Работа приложения

(кликабельно)

[![IMAGE ALT TEXT HERE](https://img.youtube.com/vi/OIV_9opfMTw/default.jpg)](https://www.youtube.com/shorts/OIV_9opfMTw)

### 1. MainActivity1

* Кнопка 1 ("Показать данные"): Запускает второе активити (MainActivity2), которое отображает все записи из таблицы "Одногруппники" в формате списка, включая ФИО и время добавления каждой записи. Используется Intent для перехода между активити.

* Кнопка 2 ("Добавить запись"): Добавляет новую запись в таблицу "Одногруппники". Временная метка устанавливается автоматически. После добавления, пользователь получает краткое уведомление.

* Кнопка 3 ("Обновить последнюю запись"): Изменяет ФИО в последней добавленной записи на "Иванов Иван Иванович". Пользователь получает уведомление об успешном или неудачном обновлении.

* Все три кнопки взаимодействуют с классом DatabaseHelper для выполнения операций с базой данных.
![alt text](https://github.com/nnka1/mobile_development.lab2/blob/main/photo_2024-11-01_19-10-37.jpg)


### 2. MainActivity2

* Отображает содержимое таблицы "Одногруппники" в TextView (activity_main2.xml).
  
* Получает данные из базы данных через DatabaseHelper.getAllData().
  
* Форматирует данные, отображая ФИО и время добавления каждой записи в читабельном виде. Используется SimpleDateFormat для форматирования временных меток.
  
* Если таблица пуста, выводит соответствующее сообщение.

![alt text](https://github.com/nnka1/mobile_development.lab2/blob/main/photo_2024-11-01_19-10-37%20(2).jpg)


  
## Как собрать проект?
1. Загрузка или клонирование репозитория:
* Скачайте файлы проекта (ZIP-архив) и разархивируйте их в удобную папку или клонируйте репозиторий с помощью команды git clone [URL репозитория].

2. Открытие проекта в Android Studio:
* Откройте Android Studio.
* В главном окне выберите "Open an existing Android Studio project".
* Найдите папку, в которую вы скачали или клонировали проект, и выберите файл build.gradle.

3. Запуск приложения:
* В Android Studio, нажмите кнопку "Run" (зеленый треугольник) на панели инструментов.
* Выберите эмулятор или подключенное Android-устройство, на котором вы хотите запустить приложение.
* Дождитесь завершения сборки и запуска приложения.

## Исходный код:
### MainActivity
```
package com.example.lab2;

import android.content.Intent;
import android.os.Bundle;
import android.view.View;
import android.widget.Button;

import androidx.activity.EdgeToEdge;
import androidx.appcompat.app.AppCompatActivity;
import androidx.core.graphics.Insets;
import androidx.core.view.ViewCompat;
import androidx.core.view.WindowInsetsCompat;

public class MainActivity extends AppCompatActivity {

    private Button button1;
    private Button button2;
    private Button button3;
    private Button button4;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        EdgeToEdge.enable(this);
        setContentView(R.layout.activity_main);

        button1 = findViewById(R.id.button1);
        button1.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                Intent intent = new Intent(MainActivity.this, Activity2.class);
                startActivity(intent);
            }
        });

        button2 = findViewById(R.id.button2);
        button2.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                Intent intent = new Intent(MainActivity.this, Activity3.class);
                startActivity(intent);
            }
        });

        button3 = findViewById(R.id.button3);
        button3.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                Intent intent = new Intent(MainActivity.this, Activity4.class);
                startActivity(intent);
            }
        });

        button4 = findViewById(R.id.button4);
        button4.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                // Закрываем приложение
                finishAffinity(); // Закрываем все активности в стеке
            }
        });
    }
}

```
### Activity2
```
package com.example.lab2;

import android.os.Bundle;

import androidx.activity.EdgeToEdge;
import androidx.appcompat.app.AppCompatActivity;
import androidx.core.graphics.Insets;
import androidx.core.view.ViewCompat;
import androidx.core.view.WindowInsetsCompat;

public class Activity2 extends AppCompatActivity {

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        EdgeToEdge.enable(this);
        setContentView(R.layout.activity_2);
        ViewCompat.setOnApplyWindowInsetsListener(findViewById(R.id.main), (v, insets) -> {
            Insets systemBars = insets.getInsets(WindowInsetsCompat.Type.systemBars());
            v.setPadding(systemBars.left, systemBars.top, systemBars.right, systemBars.bottom);
            return insets;
        });
    }
}
```
### Activity3
```
package com.example.lab2;

import android.os.Bundle;

import androidx.activity.EdgeToEdge;
import androidx.appcompat.app.AppCompatActivity;
import androidx.core.graphics.Insets;
import androidx.core.view.ViewCompat;
import androidx.core.view.WindowInsetsCompat;

public class Activity3 extends AppCompatActivity {

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        EdgeToEdge.enable(this);
        setContentView(R.layout.activity_3);
        ViewCompat.setOnApplyWindowInsetsListener(findViewById(R.id.main), (v, insets) -> {
            Insets systemBars = insets.getInsets(WindowInsetsCompat.Type.systemBars());
            v.setPadding(systemBars.left, systemBars.top, systemBars.right, systemBars.bottom);
            return insets;
        });
    }
}
```
### Activity4
```
package com.example.lab2;

import android.os.Bundle;
import android.view.View;
import android.widget.Button;

import androidx.activity.EdgeToEdge;
import androidx.appcompat.app.AppCompatActivity;
import androidx.core.graphics.Insets;
import androidx.core.view.ViewCompat;
import androidx.core.view.WindowInsetsCompat;

public class Activity4 extends AppCompatActivity {

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        EdgeToEdge.enable(this);
        setContentView(R.layout.activity_4);

        // Обработка отступов для системных элементов
        ViewCompat.setOnApplyWindowInsetsListener(findViewById(R.id.main), (v, insets) -> {
            Insets systemBars = insets.getInsets(WindowInsetsCompat.Type.systemBars());
            v.setPadding(systemBars.left, systemBars.top, systemBars.right, systemBars.bottom);
            return insets;
        });

        // Получаем ссылку на кнопку
        Button button11 = findViewById(R.id.button11);

        // Устанавливаем слушатель для события нажатия на кнопку
        button11.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                // Изменяем цвет фона кнопки при нажатии
                button11.setBackgroundTintList(getResources().getColorStateList(R.color.button_pressed_color));
            }
        });
    }
}

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
    android:background="@drawable/ass"

    tools:context=".MainActivity">

    <Button
        android:id="@+id/button1"
        android:layout_width="0dp"
        android:layout_height="0dp"
        android:layout_marginStart="12dp"
        android:layout_marginEnd="12dp"
        android:background="@drawable/transparent_background"
        android:gravity="center"
        android:text="тык раз"
        android:textAlignment="center"
        android:textAllCaps="false"
        android:textColor="@android:color/white"
        android:textSize="20dp"
        app:layout_constraintBottom_toTopOf="@id/button2"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintHeight_percent="0.2"
        app:layout_constraintHorizontal_bias="0.5"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="parent"
        app:layout_constraintVertical_bias="0"
        app:layout_constraintWidth_percent="0.75" />


    <Button
        android:id="@+id/button2"
        android:layout_width="0dp"
        android:layout_height="0dp"
        android:layout_marginStart="12dp"
        android:layout_marginEnd="12dp"
        android:background="@drawable/transparent_background"
        android:gravity="center"
        android:text="тык два"
        android:textAlignment="center"
        android:textAllCaps="false"
        android:textColor="@android:color/white"
        android:textSize="20dp"
        app:layout_constraintBottom_toTopOf="@id/button3"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintHeight_percent="0.2"
        app:layout_constraintHorizontal_bias="0.5"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toBottomOf="@id/button1"
        app:layout_constraintVertical_bias="0"
        app:layout_constraintWidth_percent="0.75" />

    <Button
        android:id="@+id/button3"
        android:layout_width="0dp"
        android:layout_height="0dp"
        android:layout_marginStart="12dp"
        android:layout_marginEnd="12dp"
        android:background="@drawable/transparent_background"
        android:gravity="center"
        android:text="тык три"
        android:textAlignment="center"
        android:textAllCaps="false"
        android:textColor="@android:color/white"
        android:textSize="20dp"
        app:layout_constraintBottom_toTopOf="@id/button4"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintHeight_percent="0.2"
        app:layout_constraintHorizontal_bias="0.5"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toBottomOf="@id/button2"
        app:layout_constraintVertical_bias="0"
        app:layout_constraintWidth_percent="0.75" />

    <Button
        android:id="@+id/button4"
        android:layout_width="0dp"
        android:layout_height="0dp"
        android:layout_marginStart="12dp"
        android:layout_marginEnd="12dp"
        android:background="@drawable/transparent_background"
        android:gravity="center"
        android:text="выйти"
        android:textAlignment="center"
        android:textAllCaps="false"
        android:textColor="@android:color/white"
        android:textSize="20dp"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintHeight_percent="0.2"
        app:layout_constraintHorizontal_bias="0.5"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toBottomOf="@id/button3"
        app:layout_constraintVertical_bias="0"
        app:layout_constraintWidth_percent="0.75" />

    <androidx.constraintlayout.widget.Guideline
        android:id="@+id/guideline"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:orientation="horizontal"
        app:layout_constraintGuide_percent="0.2" />

    <androidx.constraintlayout.widget.Guideline
        android:id="@+id/guideline2"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:orientation="horizontal"
        app:layout_constraintGuide_percent="0.42" />

    <androidx.constraintlayout.widget.Guideline
        android:id="@+id/guideline3"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:orientation="horizontal"
        app:layout_constraintGuide_percent="0.64" />

    <androidx.constraintlayout.widget.Guideline
        android:id="@+id/guideline4"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:orientation="horizontal"
        app:layout_constraintGuide_begin="629dp" />

</androidx.constraintlayout.widget.ConstraintLayout>
```
### activity2.xml
```
<?xml version="1.0" encoding="utf-8"?>
<androidx.constraintlayout.widget.ConstraintLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:id="@+id/main"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:background="@drawable/zevaet">

    <LinearLayout
        android:id="@+id/linearLayoutTop"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:orientation="horizontal"
        app:layout_constraintTop_toTopOf="parent">

        <Button
            android:id="@+id/button12"
            android:layout_width="0dp"
            android:layout_height="wrap_content"
            android:layout_weight="1"
            android:background="@drawable/transparent_background"
            android:gravity="center"
            android:text="тык"
            android:textAlignment="center"
            android:textAllCaps="false"
            android:textColor="@android:color/white"
            android:textSize="20dp"
            android:layout_margin="4dp" />

        <Button
            android:id="@+id/button13"
            android:layout_width="0dp"
            android:layout_height="wrap_content"
            android:layout_weight="1"
            android:background="@drawable/transparent_background"
            android:gravity="center"
            android:text="тык"
            android:textAlignment="center"
            android:textAllCaps="false"
            android:textColor="@android:color/white"
            android:textSize="20dp"
            android:layout_margin="4dp" />

        <Button
            android:id="@+id/button14"
            android:layout_width="0dp"
            android:layout_height="wrap_content"
            android:layout_weight="1"
            android:background="@drawable/transparent_background"
            android:gravity="center"
            android:text="тык"
            android:textAlignment="center"
            android:textAllCaps="false"
            android:textColor="@android:color/white"
            android:textSize="20dp"
            android:layout_margin="4dp" />

    </LinearLayout>

    <LinearLayout
        android:id="@+id/linearLayoutMiddle"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:layout_marginTop="300dp"
        android:orientation="horizontal"
        app:layout_constraintTop_toBottomOf="@+id/linearLayoutTop">

        <Button
            android:id="@+id/button20"
            android:layout_width="0dp"
            android:layout_height="wrap_content"
            android:layout_margin="4dp"
            android:layout_weight="1"
            android:background="@drawable/transparent_background"
            android:gravity="center"
            android:text="тык"
            android:textAlignment="center"
            android:textAllCaps="false"
            android:textColor="@android:color/white"
            android:textSize="20dp" />

        <Button
            android:id="@+id/button21"
            android:layout_width="0dp"
            android:layout_height="wrap_content"
            android:layout_weight="1"
            android:background="@drawable/transparent_background"
            android:gravity="center"
            android:text="тык"
            android:textAlignment="center"
            android:textAllCaps="false"
            android:textColor="@android:color/white"
            android:textSize="20dp"
            android:layout_margin="4dp" />

    </LinearLayout>

    <LinearLayout
        android:id="@+id/linearLayoutBottom"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:orientation="horizontal"
        android:padding="16dp"
        app:layout_constraintBottom_toBottomOf="parent">

        <Button
            android:id="@+id/button15"
            android:layout_width="0dp"
            android:layout_height="wrap_content"
            android:layout_weight="1"
            android:background="@drawable/transparent_background"
            android:gravity="center"
            android:text="тык"
            android:textAlignment="center"
            android:textAllCaps="false"
            android:textColor="@android:color/white"
            android:textSize="20dp"
            android:layout_margin="4dp" />

        <Button
            android:id="@+id/button16"
            android:layout_width="0dp"
            android:layout_height="wrap_content"
            android:layout_weight="1"
            android:background="@drawable/transparent_background"
            android:gravity="center"
            android:text="тык"
            android:textAlignment="center"
            android:textAllCaps="false"
            android:textColor="@android:color/white"
            android:textSize="20dp"
            android:layout_margin="4dp" />

        <Button
            android:id="@+id/button17"
            android:layout_width="0dp"
            android:layout_height="wrap_content"
            android:layout_weight="1"
            android:background="@drawable/transparent_background"
            android:gravity="center"
            android:text="тык"
            android:textAlignment="center"
            android:textAllCaps="false"
            android:textColor="@android:color/white"
            android:textSize="20dp"
            android:layout_margin="4dp" />
    </LinearLayout>

</androidx.constraintlayout.widget.ConstraintLayout>

```
### activity3.xml
```
<?xml version="1.0" encoding="utf-8"?>
<RelativeLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:id="@+id/main"
    android:background="@drawable/aska">


    <Button
        android:id="@+id/button"

        android:layout_width="152dp"
        android:layout_height="wrap_content"
        android:layout_alignParentStart="true"
        android:layout_alignParentTop="true"
        android:layout_marginStart="40dp"
        android:layout_marginTop="45dp"
        android:background="@drawable/transparent_background"
        android:gravity="center"
        android:text="тык"
        android:textAlignment="center"
        android:textAllCaps="false"
        android:textColor="@android:color/white" />

    <Button
        android:id="@+id/button5"
        android:layout_width="155dp"
        android:layout_height="wrap_content"
        android:layout_alignParentTop="true"
        android:layout_marginTop="45dp"
        android:layout_marginEnd="-215dp"
        android:layout_toStartOf="@+id/button7"
        android:background="@drawable/transparent_background"
        android:gravity="center"
        android:text="тык"
        android:textAlignment="center"
        android:textAllCaps="false"
        android:textColor="@android:color/white" />

    <Button
        android:id="@+id/button6"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_below="@id/button"
        android:layout_alignParentStart="true"
        android:layout_marginStart="40dp"
        android:layout_marginTop="285dp"
        android:background="@drawable/transparent_background"
        android:gravity="center"
        android:text="тык"
        android:textAlignment="center"
        android:textAllCaps="false"
        android:textColor="@android:color/white" />

    <Button
        android:id="@+id/button7"
        android:layout_width="78dp"
        android:layout_height="wrap_content"
        android:layout_below="@id/button5"
        android:layout_centerHorizontal="true"
        android:layout_marginTop="285dp"
        android:background="@drawable/transparent_background"
        android:gravity="center"
        android:text="тык"
        android:textAlignment="center"
        android:textAllCaps="false"
        android:textColor="@android:color/white" />

    <Button
        android:id="@+id/button8"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_below="@id/button6"
        android:layout_alignParentEnd="true"
        android:layout_marginTop="-48dp"
        android:layout_marginEnd="32dp"
        android:background="@drawable/transparent_background"
        android:gravity="center"
        android:text="тык"
        android:textAlignment="center"
        android:textAllCaps="false"
        android:textColor="@android:color/white" />

    <Button
        android:id="@+id/button9"
        android:layout_width="250dp"
        android:layout_height="wrap_content"
        android:layout_alignParentBottom="true"
        android:layout_centerHorizontal="true"
        android:layout_marginBottom="45dp"
        android:background="@drawable/transparent_background"
        android:gravity="center"
        android:text="тык"
        android:textAlignment="center"
        android:textAllCaps="false"
        android:textColor="@android:color/white" />

</RelativeLayout>


```
### activity4.xml
```
<?xml version="1.0" encoding="utf-8"?>
<androidx.constraintlayout.widget.ConstraintLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:id="@+id/main"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:background="#FFFFFF"
    tools:context=".Activity4">

    <Button
        android:id="@+id/button11"
        android:layout_width="206dp"
        android:layout_height="115dp"
        android:layout_margin="10dp"
        android:backgroundTint="#FFFFFF"
        android:elevation="4dp"
        android:padding="16dp"
        android:text="тык"
        android:textColor="#000000"
        android:textSize="16sp"
        android:textStyle="bold"
        app:backgroundTint="@color/colorPrimary"
        app:cornerRadius="24dp"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="parent"
        app:strokeColor="#505050"
        app:strokeWidth="6dp" />

</androidx.constraintlayout.widget.ConstraintLayout>


```
