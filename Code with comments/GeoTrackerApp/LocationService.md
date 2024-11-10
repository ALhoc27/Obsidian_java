```java
public class LocationService extends Service {

    private FusedLocationProviderClient fusedLocationClient;

    @Override
    public void onCreate() {
        super.onCreate();
        fusedLocationClient = LocationServices.getFusedLocationProviderClient(this);
        startForeground(1, getNotification());
        requestLocationUpdates();
    }

    private void requestLocationUpdates() {
        // Проверка разрешений перед запросом обновлений местоположения
        if (ContextCompat.checkSelfPermission(this, Manifest.permission.ACCESS_FINE_LOCATION) == PackageManager.PERMISSION_GRANTED
                && ContextCompat.checkSelfPermission(this, Manifest.permission.ACCESS_BACKGROUND_LOCATION) == PackageManager.PERMISSION_GRANTED) {

            LocationRequest locationRequest = LocationRequest.create()
                    .setInterval(5000) // Интервал обновлений в миллисекундах
                    .setFastestInterval(2000)
                    .setPriority(LocationRequest.PRIORITY_HIGH_ACCURACY);

            try {
                fusedLocationClient.requestLocationUpdates(locationRequest, locationCallback, Looper.myLooper());
            } catch (SecurityException e) {
                e.printStackTrace();
                // Логика для обработки отозванных разрешений или завершения службы
            }
        } else {
            // Обработка ситуации, когда разрешения не предоставлены
            Log.e("LocationService", "Необходимо разрешение для доступа к местоположению");
        }
    }

    private LocationCallback locationCallback = new LocationCallback() {
        @Override
        public void onLocationResult(LocationResult locationResult) {
            if (locationResult == null) return;
            for (Location location : locationResult.getLocations()) {
                // Обработка полученных данных о местоположении
                Log.d("LocationService", "Lat: " + location.getLatitude() + " Lng: " + location.getLongitude());
            }
        }
    };

    @Override
    public IBinder onBind(Intent intent) {
        return null;
    }
}
```

