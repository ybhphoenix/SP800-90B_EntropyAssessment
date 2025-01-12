# SP800-90B_EntropyAssessment
Cryptographic random bit generators (RBGs), also known as random number generators (RNGs), require a noise source that produces digital outputs with some level unpredictability, expressed as min-entropy. 
The SP800-90B_EntropyAssessment python package implements the min-entropy assessment methods included in the 2012 draft of Special Publication 800-90B.

##Disclaimer
This software was developed by employees of the National Institute of Standards and Technology (NIST), an agency of the Federal Government. Pursuant to title 15 United States Code Section 105, works of NIST employees are not subject to copyright protection in the United States and are considered to be in the public domain. As a result, a formal license is not needed to use the software. 

This software is provided by NIST as a service and is expressly provided "AS IS". NIST MAKES NO WARRANTY OF ANY KIND, EXPRESS, IMPLIED OR STATUTORY, INCLUDING, WITHOUT LIMITATION, THE IMPLIED WARRANTY OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE, NON-INFRINGEMENT AND DATA ACCURACY. NIST does not warrant or make any representations regarding the use of the software or the results thereof including, but not limited to, the correctness, accuracy, reliability or usefulness of the software. 

Permission to use this software is contingent upon your acceptance of the terms of this agreement.

## Requirements

This code package requires Python 2.6+ or Python 3.

##Basic Usage

There are two main files in this code package: iid_main.py and noniid_main.py. Brief usage descriptions are listed below. For further details, please refer to the user guide.

##Using iid_main.py
The file iid_main.py calls all of the tests that determine whether or not the input file appears to contain independent and identically distributed (IID) samples, and if so, gives an entropy assessment. 
The program takes three arguments: 

1. 	datafile: a binary file containing the samples to be tested.
2. 	bits_per_symbol: the number of bits required to represent the largest output symbol from the noise source. E.g., if the largest value is 12, this would be 4.
3. 	number_of_shuffles: number of shuffles for the shuffling tests to determine whether data appears to be IID. Note that too few shuffles will cause IID to fail the tests.

If the program outputs `IID = False`, try increasing number_of_shuffles (up to 1 000), or proceed to noniid_main.py.

###Examples
An example that fails (too few shuffles):

	> python iid_main.py truerand_4bit.bin 4 1
	IID = False


The same data passing when more shuffles are added:

	> python iid_main.py truerand_4bit.bin 4 10
	IID = True
	min-entropy = 3.97271
	sanity check = PASS

##Using noniid_main.py
The file noniid_main.py calls all of the min-entropy estimation methods. The program requires two arguments:

1. 	datafile: a binary file containing the samples to be tested.
2. 	bits_per_symbol: the number of bits required to represent the largest output symbol from the noise source. E.g., if the largest value is 12, this would be 4.

###Example
Non-IID estimators applied to same data as above:

	> python noniid_main.py truerand_4bit.bin 4
	min-entropy = 3.66238
	sanity check = PASS


##More Information
For more information on using this code, such as optional arguments, see the user guide in this repository.
For more information on the estimation methods, see draft SP at (http://csrc.nist.gov/publications/drafts/800-90/draft-sp800-90b.pdf).

###Contact Information
This code was originally developed by Tim Hall and is currently maintained by Kerry McKay and John Kelsey.