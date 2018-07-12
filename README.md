# Focus

**To activate the gyroscope, start with:**  
startGyroUpdates() 

**Stop registration. Finish with**  
stopGyroUpdates()

**Update interval in seconds**  
var gyroUpdateInterval: TimeInterval

**The latest sample of gyrodata**  
var gyroData. GMGyroDAta?

**The following is a function that monitors gyro-data with a given time interval.**

  func startGyros() {
   if motion.isGyroAvailable {
      self.motion.gyroUpdateInterval = 1.0 / 60.0
      self.motion.startGyroUpdates()

      // Configure a timer to fetch the accelerometer data.
      self.timer = Timer(fire: Date(), interval: (1.0/60.0), 
             repeats: true, block: { (timer) in
         // Get the gyro data.
         if let data = self.motion.gyroData {
            let x = data.rotationRate.x
            let y = data.rotationRate.y
            let z = data.rotationRate.z

            // Use the gyroscope data in your app. 
         }
      })

      // Add the timer to the current run loop.
      RunLoop.current.add(self.timer!, forMode: .defaultRunLoopMode)
   }
}

func stopGyros() {
   if self.timer != nil {
      self.timer?.invalidate()
      self.timer = nil

      self.motion.stopGyroUpdates()
   }
}


**Made from an StackOverflow thread on how to detect motion**

- (void)accelerometer:(UIAccelerometer *)accelerometer didAccelerate:(UIAcceleration *)acceleration {
    // Use a basic low-pass filter to keep only the gravity component of each axis.
    accelX = (acceleration.x * kFilteringFactor) + (accelX * (1.0 - kFilteringFactor));
    accelY = (acceleration.y * kFilteringFactor) + (accelY * (1.0 - kFilteringFactor));
    accelZ = (acceleration.z * kFilteringFactor) + (accelZ * (1.0 - kFilteringFactor));

    float accelerationThreshold = 1.01; // or whatever is appropriate - play around with different values

    if (fabs(accelX) > accelerationThreshold || fabs(accelY) > accelerationThreshold || fabs(accelZ) > accelerationThreshold) {
        [self.soundPlayer play];
        accelX = accelY = accelZ = 0;
        accelerometerActive = NO;
        accelerometer.delegate = nil;
        accelerometer = nil;
    }
}

**Inidicates if the device is stationary. Usuable?**
var stationary: Bool
