Program: Mr.Bayes ver. 3.2 (Ronquist et al., Syst. Biol. 61(3):539–542, 2012)
    http://mrbayes.sourceforge.net/index.php

For Mac you will need to install the BEAGLE library but not sure about PCs, you need as it seems that BEAGLE is already included with the PC version of the program. In any case, here the links to download and install BEAGLE: 
For Mac: https://github.com/beagle-dev/beagle-lib/wiki/MacInstallInstructions
For Windows: https://github.com/beagle-dev/beagle-lib/wiki/WindowsInstallInstructions

WINDOWS USERS: The Windows installer behaves similarly to the Macintosh installer except that it places a double-clickable executable in the MrBayes folder inside your Program directory, together with the example files and the documentation. To start the program, simply double-click on the executable. The Windows installer will also install the BEAGLE library, and it will give you a link to the relevant CUDA drivers.

We will not use it but the BEAGLE option is particularly useful if you have an NVIDIA graphics card and the relevant CUDA drivers installed, in which case MCMC sampling from amino acid and codon models should be much faster. The installer will provide you with a link that you can use to download and install the relevant drivers given that you have an NVIDIA graphics card. If the CUDA drivers are not installed (or if you do not have an NVIDIA graphics card), then BEAGLE will run on the CPU instead of on the GPU. In this case, the BEAGLE performance will be similar to that of the default likelihood calculators used by MrBayes.

