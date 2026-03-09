# SOLVE - System for Optimized Learning & automated research and Validation Engine

An automated research system that investigates, tests, and optimizes multiple approaches to solve a given machine learning problem.

## Project Overview

**Task**: Clothing Classification
**Dataset**: Fashion-MNIST (10 categories)
**Target**: Accuracy >= 0.95
**Mode**: Fully autonomous research

## Research Approaches

| Approach | Repository | Iterations | Best Accuracy | Status |
|----------|-----------|:----------:|:-------------:|:------:|
| CNN (ResBlock) | [SOLVE-approach-cnn](https://github.com/LJW0401/SOLVE-approach-cnn) | 3 | **0.9520** | PASSED |
| ResNet18 Transfer | [SOLVE-approach-resnet](https://github.com/LJW0401/SOLVE-approach-resnet) | 3 | **0.9538** | PASSED |
| EfficientNet-B0 Transfer | [SOLVE-approach-efficientnet](https://github.com/LJW0401/SOLVE-approach-efficientnet) | 1 | **0.9560** | PASSED |
| Hybrid CNN-ViT | [SOLVE-approach-vit](https://github.com/LJW0401/SOLVE-approach-vit) | 3 | **0.9518** | PASSED |

## How It Works

1. **Research**: For each approach, investigate viable architectures and training strategies
2. **Implement**: Build initial implementation with standard hyperparameters
3. **Test**: Train and evaluate on Fashion-MNIST test set
4. **Optimize**: Iteratively improve (data augmentation, hyperparameter tuning, architecture changes)
5. **Report**: Generate detailed research report for each approach

## Fashion-MNIST Categories

| Label | Category |
|-------|----------|
| 0 | T-shirt/top |
| 1 | Trouser |
| 2 | Pullover |
| 3 | Dress |
| 4 | Coat |
| 5 | Sandal |
| 6 | Shirt |
| 7 | Sneaker |
| 8 | Bag |
| 9 | Ankle boot |

## Key Conclusions

1. **EfficientNet-B0** achieved the best accuracy (0.9560) with only 1 iteration - the best out-of-the-box solution
2. **Custom CNN with residual blocks** is the most efficient approach - 0.9520 accuracy with only 2.84M parameters and fastest training
3. **ResNet18** suffered from severe overfitting; mixup augmentation was crucial to overcome it
4. **Pure ViT fails** on small datasets (0.86); CNN-Transformer hybrid is needed to reach competitive accuracy
5. All approaches benefited from **data augmentation** (flip, rotation, affine transforms)
6. **Mixup** was the most impactful single technique for improving generalization

## Reports

Detailed research reports for each approach:
- [CNN Approach Report](reports/approach_cnn.md)
- [ResNet Approach Report](reports/approach_resnet.md)
- [EfficientNet Approach Report](reports/approach_efficientnet.md)
- [ViT Approach Report](reports/approach_vit.md)
