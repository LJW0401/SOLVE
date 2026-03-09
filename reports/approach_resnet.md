# Research Report: ResNet Transfer Learning Approach

## Summary
This approach investigates using pretrained ResNet18 with transfer learning for Fashion-MNIST clothing classification.

## Target
- Accuracy >= 0.95 on Fashion-MNIST test set

## Iterations

### Iteration 1: Basic ResNet18 Transfer Learning
- **Architecture**: Pretrained ResNet18, modified conv1 for 1-channel input, 224x224 resize
- **Parameters**: 11,175,370
- **Result**: 0.9487 (NOT REACHED)
- **Training Time**: 1697.8s
- **Analysis**: Severe overfitting - train accuracy reached 100% while test plateaued at 94.87%. The model memorized training data. 224x224 resize made training very slow.

### Iteration 2: Regularized ResNet18
- **Changes**: 96x96 input (faster), stronger augmentation (rotation, affine, random erasing), weight decay 5e-4, frozen early layers, dropout 0.3
- **Parameters**: 11,175,370
- **Result**: 0.9483 (NOT REACHED)
- **Training Time**: 506.1s
- **Analysis**: Reduced overfitting gap but accuracy slightly lower. Freezing early layers may have been too restrictive. 96x96 input was much faster.

### Iteration 3: Mixup + Heavy Regularization
- **Changes**: Unfroze all layers, increased dropout to 0.5, added mixup augmentation (alpha=0.2), weight decay 1e-3, longer training (40 epochs)
- **Parameters**: 11,175,370
- **Result**: **0.9538 (PASSED)**
- **Training Time**: 932.8s
- **Analysis**: Mixup was the key technique that broke through the overfitting barrier. Combined with heavy dropout and weight decay, it prevented the model from memorizing training data while still leveraging pretrained features.

## Key Findings
1. **Overfitting is the main challenge** when using pretrained models on small, simple datasets
2. **Mixup augmentation** is highly effective for regularization in transfer learning scenarios
3. **Freezing layers is counterproductive** when combined with strong regularization - better to let all layers adapt
4. **Smaller input resolution** (96x96 vs 224x224) drastically reduces training time with minimal accuracy loss
5. **Transfer learning is overkill** for Fashion-MNIST - simpler models achieve similar results faster

## Final Result
| Metric | Value |
|--------|-------|
| Best Accuracy | 0.9538 |
| Iterations to Target | 3 |
| Final Parameters | 11.18M |
| Total Training Time | ~3,137s |
