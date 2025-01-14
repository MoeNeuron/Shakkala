# Shakkala Project V 2.0 مشروع شكّالة

<img src="images/shakkala.png" alt="Model" height="140" width="140"/>

## Introduction
Shakkala project use recurrent neural network for Arabic text vocalization to automatically form Arabic characters (تشكيل الحروف) which can be used to enhance text-to-speech systems.<br/>
This model can be used in many applications such as enhance text-to-speech systems or search results.

## Requirements
Execute following commands:<br/>
```
cd requirements
pip install -r requirements.txt
```

## Code Examples (How to)
Check full example in (demo.py) file.<br/>

1. Create Shakkala object
```
sh = Shakkala(folder_location, version={version_num})
```
2. Prepare input
```
input_int = sh.prepare_input(input_text)
```
3. Call the neural network
```
model, graph = sh.get_model()
with graph.as_default():
  logits = model.predict(input_int)[0]
```
4. Predict output
```
predicted_harakat = sh.logits_to_text(logits)
final_output = sh.get_final_text(input_text, predicted_harakat)
```
Available models: <br>

- version_num=1: First test of the solution.
- version_num=2: Main release version.
- version_num=3: Some enhancements from version number 2.

It worth to try both version_num=2 and version_num=3.

### Demo run
The fastest way to start with Shakkala by running the demo:
```
python demo.py
```

## Perfomance Tips
Shakkala built in object oriented way to load the model once into memory for faster prediction, to make sure you dont load it multiple times in your service or application follow the steps:
- Load the model in global variable:
```
sh = Shakkala(folder_location, version={version_num})
model, graph = sh.get_model()
```
- Then inside your request function or loop add:
```
input_int = sh.prepare_input(input_text)
with graph.as_default():
  logits = model.predict(input_int)[0]
predicted_harakat = sh.logits_to_text(logits)
final_output = sh.get_final_text(input_text, predicted_harakat)
```

## Accuracy
In this beta version 2 accuracy reached up to 95% and in some data it reach more based on complexity and data disribution.
This beta version trained on more than million sentences with majority of historical Arabic data from books and **some of** available formed modern data in the internet.<br/>

<img src="images/loss_history_v2.png" alt="history" style="height: 300px;"/>

### Prediction Example
For live demo based on Shakkala library click the [link](http://ahmadai.com/shakkala/) <br/>

| Real output | Predicted output |
| ------------- | ---------------- |
| فَإِنْ لَمْ يَكُونَا كَذَلِكَ أَتَى بِمَا يَقْتَضِيهِ الْحَالُ وَهَذَا أَوْلَى  | فَإِنْ لَمْ يَكُونَا كَذَلِكَ أَتَى بِمَا يَقْتَضِيهِ الْحَالُ وَهَذَا أَوْلَى |
| قَالَ الْإِسْنَوِيُّ  وَسَوَاءٌ فِيمَا قَالُوهُ مَاتَ فِي حَيَاةِ أَبَوَيْهِ أَمْ لَا  | قَالَ الْإِسْنَوِيُّ  وَسَوَاءٌ فِيمَا قَالُوهُ مَاتَ فِي حَيَاةِ أَبَوَيْهِ أَمْ لَا  |
| طَابِعَةٌ ثُلَاثِيَّةُ الْأَبْعَاد | طَابِعَةٌ ثَلَاثِيَّةُ الْأَبْعَادِ  |

### Accuracy Enhancements  
The model can be enhanced to reach more than 95% accuracy with following:<br/>
- Availability of more formed **modern**  data to train the network. (because current version trained with mostly available historical Arabic data and some modern data)
- Stack different models

## Model Design
<img src="images/mode_design.png" alt="Model"/>

## References
- A paper compare different arabic text diacritization models and show that shakkala is the best among available neural networks for this solution:
[Arabic Text Diacritization Using Deep Neural Networks, 2019](https://arxiv.org/abs/1905.01965)

## Citation
For academic work use
```
Shakkala, Arabic text vocalization, Barqawi & Zerrouki
```
OR bibtex format
```
@misc{
  title={Shakkala, Arabic text vocalization},
  author={Barqawi, Zerrouki},
  url={https://github.com/Barqawiz/Shakkala},
  year={2017}
}
```

## Contribution
### Core Team
1. Ahmad Barqawi: Neural Network Developer.<br/>
2. Taha Zerrouki: Mentor Data and Results.<br/>
### Contributors
1. Zaid Farekh & propellerinc.me: Provide infrastructure and consultation support.<br/>
2. Mohammad Issam Aklik: Artist.<br/>
3. Brahim Sidi: Form new sentences.<br/>
4. Fadi Bakoura: Aggregate online content.<br/>
5. Ola Ghanem: Testing.<br/>
6. Ali Hamdi Ali Fadel: Contribute code.<br/>

License
-------
Free to use and distribute only mention the original project name Shakkala as base model.<br/>

  The MIT License (MIT)

  Copyright (c) 2017 Shakkala Project

  Permission is hereby granted, free of charge, to any person obtaining a copy
  of this software and associated documentation files (the "Software"), to deal
  in the Software without restriction, including without limitation the rights
  to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
  copies of the Software, and to permit persons to whom the Software is
  furnished to do so, subject to the following conditions:

  The above copyright notice and this permission notice shall be included in all
  copies or substantial portions of the Software.
