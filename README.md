# VisDial-ES: Spanish Visual Dialog Dataset

The first Visual Dialog dataset in Spanish, containing approximately **1.2 million dialog question-answer pairs** about image-grounded conversations.

## 📊 Dataset Overview

VisDial-ES is the Spanish version of the Visual Dialog v1.0 dataset, created through systematic machine translation and validated with human evaluation. This dataset enables research in multilingual visual understanding and Spanish-language multimodal AI systems.


### Translation Quality Scores

Based on human evaluation (3-point scale):

- **Fluency**: 2.91 / 3.0
- **Adequacy**: 2.93 / 3.0
- **Coherence**: 2.88 / 3.0

## 📥 Download

### Files in this Repository

```
visdial-es-spanish/ 
├── visdial_1.0_val_ES.json      
└── visdial_1.0_test_ES.json     
```

**⚠️ Important**: The training set (`visdial_1.0_train_ES.json`) is very large (>2GB) and is hosted separately.


### Quick Download

```bash
# Clone the repository
git clone https://github.com/IMScience-PPGINF-PucMinas/visdial-es-spanish

cd visdial-es-spanish
```


**Getting training data:**

Manually download the visdial_1.0_train_ES.json file
[https://huggingface.co](https://huggingface.co/datasets/milenaadao/visdial-es-spanish/tree/main)

Place the training set you downloaded from HuggingFace inside the ```visdial-es-spanish``` folder

## 📋 Dataset Structure

Each JSON file follows the VisDial v1.0 format:

```json
{
  "version": "1.0",
  "data_type": "train",
  "data": {
    "questions": [
      "¿Cuántas personas hay en el sofá?",
      "¿Cuáles son sus géneros?",
      ...
    ],
    "answers": [
      "Dos",
      "Un hombre y una mujer",
      ...
    ],
    "dialogs": [
      {
        "image_id": 123456,
        "caption": "Un grupo de personas jugando fútbol en el campo",
        "dialog": [
          {
            "question": 0,
            "answer": 5,
            "answer_options": [2, 5, 8, 12, 15, ...]
          },
          ...
        ]
      },
      ...
    ]
  }
}
```

### Field Descriptions

- **`questions`**: List of all unique questions in Spanish
- **`answers`**: List of all unique answers in Spanish
- **`dialogs`**: List of dialog instances, each containing:
  - `image_id`: COCO/Flickr image identifier
  - `caption`: Image caption in Spanish
  - `dialog`: List of 10 question-answer rounds
    - `question`: Index into the questions list
    - `answer`: Index into the answers list (ground truth)
    - `answer_options`: List of 100 candidate answer indices

## 🚀 Quick Start

### Loading the Dataset

```python
import json

# Load validation set
with open('visdial_1.0_val_ES.json', 'r', encoding='utf-8') as f:
    data = json.load(f)

# Access components
questions = data['data']['questions']
answers = data['data']['answers']
dialogs = data['data']['dialogs']

# Example: First dialog
first_dialog = dialogs[0]
print(f"Caption: {first_dialog['caption']}")
print(f"Image ID: {first_dialog['image_id']}")

# First question-answer pair
qa_round = first_dialog['dialog'][0]
question_idx = qa_round['question']
answer_idx = qa_round['answer']

print(f"Q: {questions[question_idx]}")
print(f"A: {answers[answer_idx]}")
```

### Example Dialog

```python
Caption: "Un grupo de personas jugando fútbol en el campo"

Q1: ¿Se ven como si se estuvieran divirtiendo?
A1: Difícil de decir, están en el medio del juego es un juego con 2 equipos diferentes

Q2: ¿Están vestidos con uniformes?
A2: Sí, cada uno tiene un uniforme diferente

Q3: ¿Cuál está sosteniendo la pelota?
A3: La mujer
```

## 🔬 Research Applications

This dataset enables research in:

- **Multilingual Visual Dialog**: Training and evaluating Spanish visual dialog systems
- **Cross-lingual Transfer**: Studying knowledge transfer between English and Spanish
- **Multimodal Understanding**: Developing Spanish vision-language models
- **Cultural Adaptation**: Investigating language-specific visual reasoning patterns
- **Low-resource NLP**: Advancing Spanish multimodal AI capabilities

## 🛠️ Translation Pipeline

This dataset was created using a systematic translation pipeline. To translate other datasets or customize the translation:

**Pipeline Repository**: [github.com/IMScience-PPGINF-PucMinas/visdial-translation-pipeline](https://github.com/IMScience-PPGINF-PucMinas/visdial-translation-pipeline.git)

Translation method:
- Model: `Helsinki-NLP/opus-mt-en-es` (MarianMT)
- Batch processing with GPU acceleration
- Human validation on random samples
- Preserved original dataset structure

## 📊 Baseline Results

### Using LLaVA-7B

| Model | NDCG | MRR | R@1 | R@5 | R@10 |
|-------|------|-----|-----|-----|------|
| LLaVA-7B (English) | 75.5 | 84.2 | 82.7 | 83.7 | 85.9 |
| LLaVA-7B (Spanish) | 85.3 | 88.4 | 96.4 | 96.4 | 98.6 |


*Initial baseline 

## 🖼️ Image Data

This dataset references images from:
- **MS COCO**: [https://cocodataset.org/](https://cocodataset.org/)
- **Flickr**: Available through VisDial official download

**Note**: This repository contains only the textual dialogs. You need to download the images separately from the original VisDial dataset.

### Downloading Images

```bash
# Download COCO images
wget http://images.cocodataset.org/zips/train2014.zip
wget http://images.cocodataset.org/zips/val2014.zip

# Download VisDial Flickr images
# Visit: https://visualdialog.org/data
```

## 📖 Citation

If you use this dataset in your research, please cite:

```bibtex
@inproceedings{adao2025multilingual,
  title={Multilingual Visual Understanding: Extending Visual Dialog to Portuguese and Spanish Through Cross-Modal Adaptation},
  author={Ad{\~a}o, Milena Menezes and Guimar{\~a}es, Silvio Jamil F. and Patroc{\'\i}nio Jr, Zenilton K. G.},
  booktitle={Progress in Pattern Recognition, Image Analysis, Computer Vision, and Applications (CIARP)},
  year={2025}
}
```


## 📄 License

This dataset is released under the [MIT License](LICENSE).

**Note**: The dataset inherits licensing terms from the original VisDial dataset. Please ensure compliance with both MS COCO and Flickr image licenses when using the visual data.

## 🤝 Contributing

Found an issue or want to improve the translations? 

- **Report issues**: [Open an issue](https://github.com/IMScience-PPGINF-PucMinas/visdial-es-spanish/issues)
- **Improve translations**: See our [Translation Pipeline](https://github.com/IMScience-PPGINF-PucMinas/visdial-translation-pipeline)
- **Share results**: We'd love to hear about your research!

## 🔗 Related Resources

- **Portuguese Dataset**: [VisDial-PT](https://github.com/IMScience-PPGINF-PucMinas/visdial-pt-brazilian)
- **Original VisDial**: [visualdialog.org](https://visualdialog.org/)
- **Paper**: CIARP 2025


**Authors:**
- Milena Menezes Adão 
- Silvio Jamil F. Guimarães  
- Zenilton K. G. Patrocínio Jr 

**Institution:** Pontifícia Universidade Católica de Minas Gerais – Belo Horizonte, Brazil


**Note**: This is a research dataset. If you use it in production systems, please ensure proper evaluation and validation for your specific use case.