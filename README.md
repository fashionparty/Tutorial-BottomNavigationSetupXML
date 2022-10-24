### 1) Dodaj NavHostFragment i BottomNavigationView do MainActivity. Pamiętaj że NavHostFragment musi mieć ustawiony **konkretny parametr name** tak jak pokazano poniżej:


**res/layout/activity_main.xml**
```
<fragment
  android:id="@+id/fragment_main"
  android:name="androidx.navigation.fragment.NavHostFragment"
  app:navGraph="navgiation/navigation_bnv"
  layout:constraint(...) />
  
<com.google.android.material.bottomnavigation.BottomNavgationView
  android:id="@+id/bnv"
  app:menu="@menu/menu_bnv"
  layout:constraint(...) />
```

### 2) Stwórz dokumenty menu i nawigacji. ID'ki opcji w menu i fragmentów muszą być identyczne:


**res/menu/menu_bnv.xml**
```
<item 
  android:id="@+id/navigation_a"
  android:icon="@drawable/icon_a"
  android:title="A" />
<item
  android:id="@+id/navigation_b" 
  (...)
```

**res/navigation/navigation_bnv.xml**
```
app:startDestination="@id/navigation_home">

<fragment
  android:id="@+id/navigation_a"
  android:label="A"
  android:name="com.example.project.AFragment"
  tools:layout="@layout_fragment_a" />
<fragment
  android:id="@+id/navigation_b"
  (...)
```
  
### 3) Skonfiguruj Navigation Controller w głównej aktywności:

**MainActivity.kt**
```
private fun setupBottomNavbar() {
  val navView = mBinding.bnv
  val navController = findNavController(R.id.fragment_main)
  val appBarConfiguration = AppBarConfiguration(
    setOf(
      R.id.navigation_a,
      R.id.navigation_b,
      (...)
    )
  )
  setupActionBarWithNavController(navController, appBarConfiguration)
  navView.setupWithNavController(navController)
}
```
