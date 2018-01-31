

    motion.attitude.roll
    motion.atttiude.pitch
    motion.attitude.yaw

#problem with measurement during gimbol lock (when phones are vertical)

#to solve use quaternion

     float yaw = asin(2*(quat.w*quat.y - quat.x*quat.z ));
     float roll = atan2(2*(quat.y*quat.w - quat.x*quat.z), 1 - 2*quat.y*quat.y - 2*quat.z*quat.z);
     float pitch = atan2(2*(quat.x*quat.w + quat.y*quat.z), 1 - 2*quat.x*quat.x - 2*quat.z*quat.z); 

#use following if you want angle to go over 90 

    float roll = atan(2*(quat.y*quat.w - quat.x*quat.z)) * 2;
    float pitch = atan(2*(quat.x*quat.w + quat.y*quat.z)) * 2;
