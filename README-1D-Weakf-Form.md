
# 1D-Weak-Form_Complete

## Model tree
![Pasted image 20220718215524](https://user-images.githubusercontent.com/70443015/180076407-84a3b985-216e-4297-8e38-00c37fa01779.png)

### Component 1 - Physics
Component 1 - Physics carries the 1D formulation (dissertation, chapter 3). 

#### Geometry 1 and Domains
![Pasted image 20220718222612](https://user-images.githubusercontent.com/70443015/180076516-ae20a351-1a3d-4f00-9c13-75447f2b0386.png)
![Pasted image 20220718225519](https://user-images.githubusercontent.com/70443015/180076560-f2b2c096-a720-4b93-a187-b3c9bc993f8b.png)


### Axisymmetric
Carries all definitions for extrusion.

Make sure the interpolations nLegendre<Pump,Stokes,etc> point to a valid file. If you don't have the numeric Legendre polinomials, you can first run the method Database_gen in the file AssociatedLegendreDatabase.mph.

### How to run? -- Method Call LoopUpdatingLeg
Under Global Definitions you will find the method LoopUpdatingLeg. This method is farily complete but asks for many inputs, which can be daunting at first (see [Input list](#input-list)).

![Pasted image 20220720161544](https://user-images.githubusercontent.com/70443015/180076656-f9b0aaf8-fe30-46a9-b19e-6f5fc6e4800a.png)


## Input list

#### (string) pathLegendreDatabase
refers to the local path where the Legendre polinomials database is stored. 

The following inputs define a sweep over the external layer thickness (parameter 'ta' in the Globa Definitions > Parameters - General tab)
#### (float) **alumina initial loop thickness**: 
first 'ta' value in the sweep
#### (float) **alumina final loop thickness**: 
upper 'ta' limit for the sweep
#### (float) **alumina thickness loop step**: 
'ta' is incremented by this value over each iteration.

We also define the inner layers defined above. This was built to support studies of spheres coated with multiple layers.
#### (float) **tb**, gap thickness: 
center layer thickness
#### (float) **tc**:
inner layer thickness

Output file management definitions:
#### (bool) **Output txt files with results**: 
if true will create a text file with output data to be defined.
#### (string) **observation/filename tag**: 
a string with any information/observation/slash comment that will define the output files basenames.
#### (string) **filePath**: 
path where the output file is to be saved. The output file will be save as filePath/observation_tai<[alumina initial loop thickness](#float-alumina-initial-loop-thickness)>nm_taf<[alumina final loop thickness](#float-alumina-final-loop-thickness>nm.txt
#### (string array) **List of Expressions to Evaluate and Output in .txt file** :  
defines the expression to evaluate. It should contain comsol functions, global parameters or component 1 probes (Component 1 - Physics > Definitions>Probes)

![Pasted image 20220718232400](https://user-images.githubusercontent.com/70443015/180076879-78e3f6b5-5a04-485c-8952-137d278111a1.png)

#### (bool)  **Output png files**:
if true will generate plots (of quantities defined on [List of (tag, expressions) for png outputs](#string-array-list-of-tag-expression-for-png-outputs))
#### (string) **imgFolder**: 
relative path inside ==filePath== where plots defined by expressions on [List of tags](#string-array-list-of-tag-expression-for-png-outputs) will be stored.
#### (string array) List of (tag, expression) for png outputs
First column defines the png file name. Second column defines the expression to evaluate. It should be variables defined on the Axisymmetric component (*comp1*).

![Pasted image 20220718231629](https://user-images.githubusercontent.com/70443015/180077042-046065c3-b56f-4088-b4df-1a9a256b413d.png)

#### (bool) setColorRange
if true will fiz color range in png images
#### (float) cmin
value for color range minimum
#### (float) cmax
value for color range maximum
