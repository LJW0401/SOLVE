# Research Report: Vision Transformer (ViT) Approach

## Summary
This approach investigates using Vision Transformers for Fashion-MNIST classification, starting from a pure ViT and evolving to a hybrid CNN-Transformer architecture.

## Target
- Accuracy >= 0.95 on Fashion-MNIST test set

## Iterations

### Iteration 1: Pure Small ViT
- **Architecture**: Custom ViT with 4x4 patches, 256-dim embeddings, 8 heads, 6 layers, trained from scratch on 28x28 images
- **Parameters**: 4,759,050
- **Result**: 0.8628 (NOT REACHED)
- **Training Time**: 892.0s
- **Analysis**: Pure ViT failed badly on small dataset. Without pretrained features, the attention mechanism couldn't learn useful representations from 28x28 grayscale images. The model underfitted severely.

### Iteration 2: Hybrid CNN-ViT
- **Changes**: Added CNN stem (2 conv blocks extracting 192-dim features at 7x7 resolution), reduced transformer to 4 layers with 192-dim, warmup + cosine LR
- **Parameters**: 2,124,810
- **Result**: 0.9455 (NOT REACHED)
- **Training Time**: 998.2s
- **Analysis**: Massive improvement (+0.08). CNN stem provided the inductive biases that pure ViT lacked. The transformer then refined spatial relationships. Close to target but plateaued.

### Iteration 3: Enhanced Hybrid CNN-ViT
- **Changes**: Larger model (256-dim, 8 heads, 6 layers), deeper CNN stem (5 conv layers), mixup augmentation, heavier weight decay (1e-3), 100 epochs
- **Parameters**: 5,309,514
- **Result**: **0.9518 (PASSED)**
- **Training Time**: 3085.5s
- **Analysis**: The combination of a strong CNN feature extractor with transformer attention layers proved effective. Mixup prevented overfitting during the long training. Reached target around epoch 70.

## Key Findings
1. **Pure ViT is unsuitable** for small datasets and low-resolution images - requires either pretraining or CNN hybridization
2. **CNN stem is essential** - provides the local feature extraction that transformers can't learn from scratch on small data
3. **Hybrid architecture works** but is less efficient than pure CNN or transfer learning for this task
4. **Long training required** - ViT took 100 epochs vs 60 for CNN to converge
5. **Transformer attention adds value** on top of CNN features, but the marginal gain vs pure CNN is small

## Architecture Evolution
```
Pure ViT (0.86) → Hybrid CNN-ViT (0.94) → Enhanced Hybrid (0.95)
```

## Final Result
| Metric | Value |
|--------|-------|
| Best Accuracy | 0.9518 |
| Iterations to Target | 3 |
| Final Parameters | 5.31M |
| Total Training Time | ~5,975s |
