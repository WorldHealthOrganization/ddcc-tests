# Creating and Using Fake Data

Three approaches are used to create test data.

## Examples in IGs

Initial authors should be encourated to create at least one instance of fake data. Fake data is often provided in IGs and is a recommended best practice. 

One simple instance can be turned into a handful easily. The DDCC IG contains simple example data instances that were authored based on the singular instance but expanded to six examples using the six official UN languages.
```sh
input/fsh
├── example-arabic.fsh
├── example-chinese.fsh
├── example-english.fsh
├── example-french.fsh
├── example-russian.fsh
└── example-spanish.fsh
```

## FSH Templates

If more data are needed, such as for load testing, they can be created by templating a working FSH file. Consider this example from the DDCC IG:
```
Instance:     DDCC-Patient-Arabic
InstanceOf:   DDCCPatient
Usage:        #example
* name[+].text = "أولوس أجيريوس"
* name[=].use = #official
* birthDate = "2003-03-03"

Instance: DDCC-Organization-Arabic
InstanceOf: DDCCOrganization
Usage: #example
* name = "مستشفى حكومي"
...
```
The required unique bits of IDs can be substituted with a templating language. Here Jinja2 template variables are used:
```txt
Instance:     DDCC-Patient-{{suffix}}
InstanceOf:   DDCCPatient
Usage:        #example
* name[+].text = "{{name}}"
* name[=].use = #official
* birthDate = "{{birthDate}}"

Instance: DDCC-Organization-{{suffix}}
InstanceOf: DDCCOrganization
Usage: #example
* name = "{{orgname}}"
```
Then using a scripting language, copies of the template can be made and new values inserted. See [here](https://github.com/intrahealth/bulk-fsh) a fully worked example repository that creates DDCC bulk data compatible with the IG. It will need to be modified for other IGs.

## Fake Names and Demographics

For testing, bulk data may require names, locations, demographical details, and other information. For a slim IG like DDCC, fake names for bulk tests are created from the periodic table of the elements using a [Python script](https://github.com/intrahealth/synthea-elements/blob/main/prepare-elements-names.ipynb) and the Google Translate API.

This is only one approach to neutral naming schemes. For realistic, time-series medical records with real locations see the [Synthea project](https://github.com/synthetichealth/synthea).

```txt
neutron neutrón neutron نيوترون 中子 нейтрон
hydrogen hidrógeno hydrogène هيدروجين 氢 водород
helium helio hélium الهيليوم 氦 гелий
lithium litio lithium الليثيوم 锂 литий
beryllium berilio béryllium البريليوم 铍 бериллий
boron boro bore البورون 硼 бор
carbon carbón carbone كربون 碳 углерод
nitrogen nitrógeno azote نتروجين 氮 азот
oxygen oxígeno oxygène الأكسجين 氧 кислород
fluorine flúor fluor الفلور 氟 фтор
neon neón néon نيون 氖 неон
sodium sodio sodium صوديوم 钠 натрий
magnesium magnesio magnésium المغنيسيوم 镁 магний
aluminum aluminio aluminium الألومنيوم 铝 алюминий
silicon silicio silicium السيليكون 硅 кремний
phosphorus fósforo phosphore الفوسفور 磷 фосфор
sulfur azufre soufre كبريت 硫 сера
chlorine cloro chlore الكلور 氯 хлор
argon argón argon الأرجون 氩气 аргон
potassium potasio potassium البوتاسيوم 钾 калий
...
```

## Sushi Performance

> Note that performance testing showed that using a single-threaded process like Sushi to build FHIR Shorthand templates into 1000s of records has substantial limits above a few thousand records. In the below test result, a recent workstation was used to run Sushi on X records. Each FSH record had 8 FHIR resources.

```log
Num FSH files: 1, Elapsed time: 0:08.57, CPU: 26%, Max RAM (KB): 195316
Num FSH files: 10, Elapsed time: 0:07.20, CPU: 59%, Max RAM (KB): 198180
Num FSH files: 50, Elapsed time: 0:13.99, CPU: 87%, Max RAM (KB): 237368
Num FSH files: 100, Elapsed time: 0:25.30, CPU: 96%, Max RAM (KB): 243532
Num FSH files: 250, Elapsed time: 1:13.59, CPU: 101%, Max RAM (KB): 301560
Num FSH files: 500, Elapsed time: 3:23.37, CPU: 102%, Max RAM (KB): 430272
Num FSH files: 1000, Elapsed time: 11:36.11, CPU: 104%, Max RAM (KB): 720144
Num FSH files: 1500, Elapsed time: 26:22.21, CPU: 103%, Max RAM (KB): 717560
Num FSH files: 2000, Elapsed time: 48:41.10, CPU: 103%, Max RAM (KB): 1103084
Num FSH files: 2500, Elapsed time: 1:18:21, CPU: 103%, Max RAM (KB): 1123668
```