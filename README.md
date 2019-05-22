# Conversion of OBJ to STL

This folder contains meshes to be converted to STL format for use in Gazebo7.

This is because Gazebo7 does not support the OBJ format, only Gazebo 7.4. Upgrading to Gazebo7.4 is possible but ill-advised as it might break some things that otherwise worked well in the ROS Kinetic install.

The `Meshes to be Edited` folder is the working folder for conversion.

Most of the models can be found in `/home/ubuntu/Downloads/osrf-gazebo_models-e6d645674e8a`. If not, they can be downloaded here: [OSRF Gazebo Model Repo](https://bitbucket.org/osrf/gazebo_models/downloads/)

The models can also be found installed in `/home/ubuntu/.gazebo/models` where they can then be accessed by Gazebo itself.

## Steps

Get the OBJ models from `/model_name/meshes/model_name.obj`

1. Import them into blender via the import dialog

2. Export them as STL in blender via the export dialog

3. Place the exported the STL into the the same folder as the OBJ (deletion of the original OBJ file is optional)

4. Open up `/model_name/model.sdf`. It should look something like this:

   ```xml
   <?xml version="1.0" ?>
   <sdf version="1.6">
     <model name="ambulance">
       <static>true</static>
       <link name="link">
         <collision name="collision">
           <geometry>
             <mesh>
               <scale>0.0254 0.0254 0.0254</scale>
               <uri>model://model_name/meshes/model_name.obj</uri>
             </mesh>
           </geometry>
         </collision>
         <visual name="visual">
           <geometry>
             <mesh>
               <scale>0.0254 0.0254 0.0254</scale>
               <uri>model://model_name/meshes/model_name.obj</uri>
             </mesh>
           </geometry>
         </visual>
       </link>
     </model>
   </sdf>
   
   ```

   5. Replace all instances of `model://model_name/meshes/model_name.obj` with `model://model_name/meshes/model_name.stl`.
   6. It should now be possible to load the model into Gazebo7.

