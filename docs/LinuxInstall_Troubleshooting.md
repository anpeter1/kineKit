# Steps used to install DLC on Lambda Quad

Download .yaml file and unpack in 'Downloads' (as is, did not yet change anything in the yaml file)

Navigate to 'Downloads' folder

      cd ~/Downloads
      
Create Enviornment (use -n to designate env name, here DLC_troubleshoot)

    conda env create -n DLC_troubleshoot -f DEEPLABCUT.yaml

Here installation fails due to wxpython,need to remove and reinstall DLC

    conda remove --name DLC_troubleshoot --all

Open the .yaml file and change deeplabcut[gui] to deeplabcut, save file

Re-create Enviornment

    conda env create -n DLC_troubleshoot -f DEEPLABCUT.yaml

Installation is succussful, activate with:

    conda activate DLC_troubleshoot

When you try to run

    python -m deeplabcut

You get the error "You installed DLC lite, thus GUI's cannot be used. If you need GUI support please: pip install 'deeplabcut[gui]''", so we still need to install wx python

~~While still in the env, install wxpython by running~~

~~conda install -c conda-forge wxpython~~

~~If you try to activate the gui again you get the error, "ImportError: Numba needs NumPy 1.22 or less"~~

The above instructions are for an installation prior to an update to Numpy, which is not too high for DLC (must be less than 1.22 as of Aug 18th, 2022). Wxpython was also updated as of Aug 8th 2022 (4.2.0), but our current versions of DLC that are working use 4.1.1, so I have used that installation below.

To install the previous version of wxpython run (inside your DLC env!):

    conda install -c conda-forge wxpython==4.1.1 

After installing, need to install the lower version of numpy (inside your DLC env!):

    conda install -c conda-forge numpy==1.21.5

When prompted with "the following packages will be SUPERSEDED by a higher-priority channel", enter 'Y', DLC will run with the lower version of numpy

You can check the numpy version by running the following

    ipython
    import wx
    import numpy
    wx.__version__
    numpy.__version__
    exit()

Now you can launch Deeplabcut GUI with:

    python -m deeplabcut

