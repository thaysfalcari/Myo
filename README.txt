
July 3, 2018

System Requirements:

- A running POSIX operating system, with bash shell
- MATLAB software, containing fitcsvm function
- GNU Octave installed

In this repository you will find a dataset with sEMG signals
collected from 5 participants. Each partipant folder contains 20 sEMG
recorded waves with 8 channels, that correspond to columns in .txt
files.

During execution, you must be at the root of this file tree on the
directory amostras_6_Gestos.


Steps for programs execution:

First:
Execute the program: chamaMontaMatrizDeTxtParaAscii.sh
This program will divide the sEMG signals of .txt files in two time
windows of 0.64s and 1.28s, in which the number of lines will be 128
and 256, respectivelly.

In the end of the execution files named as
emgAmostraXX_janela_XX_tamanho_128.ascii
emgAmostraXX_janela_XX_tamanho_256.ascii will be generated inside
participant directory.

Second:
Execute the program: chamaMontaVetoresRMS.sh
This program will calculate the RMS value of each window, for each
channel, that was previously generated.
The GNU Octave is the software called to calculate the RMS
values. Then, it must be installed in your system.

After the execution the file
emgAmostraXX_janela_XX_tamanho_128_VetorRMS.ascii for 0.64s time
window, and emgAmostraXX_janela_XX_tamanho_256_VetorRMS.ascii for
1.28s time window.

Third:
Execute the program: montaArqSVM.sh
This program will separate the train dataset from the test one.

After execution the following files will be generated:
-VetRMS_Treino_256_semRotulos.ascii
-VetRMS_Treino_256_semRotulos_embaralhado.ascii
-treino_18_primeirosVetRMS_256_semRotulos_embaralhado.ascii

Fourth:
Execute the program: montaConjuntoTreinoEClass.sh
This program will assemble the files generated in the previous
execution to compose the final dataset for training and test that will
be used as SVM arguments.

In the end of the execution the following files will be generated:
- conjuntoTeste_128.ascii
- conjuntoTreino_128.ascii
- conjuntoTeste_256.ascii
- conjuntoTreino_256.ascii



Finally to classify the data you will use program svmTrain.m,
which is a MATLAB script.
You must be at the root of this file tree on the
directory amostras_6_Gestos.

DATA
- conjuntoTeste_128.ascii
- conjuntoTreino_128.ascii
- conjuntoTeste_256.ascii
- conjuntoTreino_256.ascii

LABELS
- rotulosTeste_128.txt
- rotulosTreino_128.txt
- rotulosTeste_256.txt
- rotulosTreino_256.txt

The labels files must be copied in all participant directories.

In the end of this execution, the best SVM models will be saved to
compose the SVM cascade.

The SVM cascade program is named as svmCascade_v2.m and its sequence
is changed according to the best SVM models found.
To execute the SVM cascade it will be necessary to add the following
labels files in the same directory of the SVM models.

LABELS
- rotulosTeste_clenchingv2.txt
- rotulosTeste_pointingv2.txt
- rotulosTeste_relaxingv2.txt
- rotulosTeste_spreadingv2.txt
- rotulosTeste_waveInv2.txt
- rotulosTeste_waveOutv2.txt


For more information or doubts about this procedure you may get in
touch by e-mail: thays.falcari@gmail.com






