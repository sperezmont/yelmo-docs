# Running with YelmoX-REMBO

*Before doing anything, make sure dependencies are installed (Lis, NetCDF, Python:runner)*

## Step 1: Clone the repositories

```bash
# Clone repository: YelmoX
git clone https://github.com/palma-ice/yelmox.git

# Clone yelmo into a sub-directory too
cd yelmox
git clone https://github.com/palma-ice/yelmo.git

# Clone isostasy into a sub-directory too 
git clone https://github.com/palma-ice/isostasy.git

# Clone rembo into a sub-directory too 
git clone https://github.com/alex-robinson/rembo1
```

At this point all the code is downloaded onto the machine.
Now we need to configure it for compiling properly.

## Step 2: Run configuration scripts for each code base

```bash
# Enter Yelmo directory and configure it for compiling
cd yelmo
python config.py config/snowball_gfortran
make clean
cd ..

# Enter isostasy directory and configure it for compiling 
cd isostasy
python config.py config/snowball_gfortran
make clean
cd ..

# Enter rembo1 directory and configure it for compiling 
cd rembo1
python config.py config/snowball_gfortran
make clean
cd ..

# From YelmoX directory, configure it for compiling too
python config.py config/snowball_gfortran
make clean 
```

Note that the example assumes we are using the machine called `snowball` and
we will use the compiler `gfortran`. If this is not correct, you will need
to use the right configuration file available in the `config/` directory, or
make your own using the others as a template.

## Step 3: Compile the default program

```bash
make clean 
make yelmox_rembo
```

## Step 4: Make a link to `ice_data`

```bash
# Link to `ice_data` repository wherever you have it saved on your system
ln -s /media/Data/ice_data

# Take a look at some data to make sure it worked well
ncview ice_data/Greenland/GRL-16KM/GRL-16KM_TOPO-M17-v5.nc
```

## Step 5: Run a test simulation

```bash
# Run a test simulation of Greenland for 100 yrs
./runme -r -e rembo -n par/yelmo_Greenland_rembo.nml -o output/test1 -p ctrl.time_end=1e2
```

That's it, YelmoX-REMBO is working.
