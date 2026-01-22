# CLAUDE.md - AI Assistant Guide for Machine_Learning Repository

## Repository Overview

This is a Machine Learning repository intended for developing, training, and deploying machine learning models and experiments.

**Current State**: Early stage repository - structure and conventions will evolve as the project grows.

**Primary Purpose**: Machine learning experimentation, model development, and research

## Repository Structure

### Expected Directory Organization

```
Machine_Learning/
├── data/                   # Data storage (should be .gitignored)
│   ├── raw/               # Original, immutable data
│   ├── processed/         # Cleaned and transformed data
│   └── external/          # Third-party data sources
├── notebooks/             # Jupyter notebooks for exploration and analysis
│   ├── exploratory/      # Initial data exploration
│   └── experiments/      # Model experiments and prototyping
├── src/                   # Source code for use in this project
│   ├── data/             # Data loading and processing scripts
│   ├── features/         # Feature engineering code
│   ├── models/           # Model architectures and training code
│   ├── evaluation/       # Model evaluation and metrics
│   └── utils/            # Utility functions and helpers
├── models/                # Trained model artifacts (should be .gitignored or versioned separately)
├── tests/                 # Unit and integration tests
├── configs/               # Configuration files (hyperparameters, paths, etc.)
├── scripts/               # Standalone scripts for training, evaluation, etc.
├── docs/                  # Documentation
├── requirements.txt       # Python dependencies
├── environment.yml        # Conda environment specification (if using conda)
├── setup.py              # Package installation configuration
└── .gitignore            # Git ignore rules

```

**Note**: This structure is aspirational - not all directories exist yet. Create them as needed.

## Development Workflows

### 1. Data Management

- **NEVER commit large datasets** to git - use `.gitignore` for data directories
- Store raw data separately from processed data
- Document data sources and preprocessing steps
- Consider using DVC (Data Version Control) or similar tools for data versioning
- Keep data loading code separate from model code

### 2. Experiment Tracking

- Use descriptive names for experiments and notebook files
- Include dates in experiment notebook names (e.g., `2026-01-22_initial_baseline.ipynb`)
- Log hyperparameters, metrics, and results systematically
- Consider using MLflow, Weights & Biases, or TensorBoard for experiment tracking
- Document failed experiments and lessons learned

### 3. Model Development

**Prototyping Phase:**
- Start in Jupyter notebooks for exploration
- Keep notebooks organized and well-documented
- Clear outputs before committing notebooks (use `nbstripout` or similar)

**Production Phase:**
- Refactor working code from notebooks into Python modules
- Write modular, reusable code in `src/` directory
- Separate data processing, model architecture, training, and evaluation
- Use configuration files for hyperparameters and settings

### 4. Code Quality

- Write unit tests for data processing and model utilities
- Use type hints for function signatures
- Follow PEP 8 style guidelines for Python code
- Add docstrings to functions and classes
- Keep functions focused and single-purpose
- Avoid hardcoded paths - use configuration files or environment variables

### 5. Version Control

**Commit Practices:**
- Make frequent, small commits with descriptive messages
- Commit format: `<type>: <description>`
  - Types: `feat`, `fix`, `data`, `model`, `experiment`, `refactor`, `test`, `docs`, `config`
  - Examples:
    - `feat: add LSTM model architecture`
    - `data: add preprocessing pipeline for text data`
    - `experiment: baseline random forest with default params`

**Branching:**
- Use feature branches for new models or significant changes
- Branch naming: `feature/<description>`, `experiment/<model-name>`, `fix/<issue>`
- Current branch: `claude/claude-md-mkpwc72u91n077xd-Vtz2D`

## Key Conventions

### Python Dependencies

- Maintain `requirements.txt` with pinned versions for reproducibility
- Use virtual environments (venv, conda, or poetry)
- Document Python version requirements
- Separate development dependencies if needed

### Configuration Management

- Store hyperparameters in config files (YAML, JSON, or Python config classes)
- Use environment variables for sensitive information (API keys, credentials)
- Never commit credentials or API keys
- Use `.env` files with `.gitignore` for local configuration

### Model Artifacts

- Save trained models with versioning (include date, version, or experiment ID)
- Store model metadata (hyperparameters, training date, metrics)
- Use standardized formats (pickle, joblib, SavedModel, ONNX)
- Consider model registry for production models
- Document model performance metrics

### Jupyter Notebooks

- Use clear markdown cells to explain analysis steps
- Keep notebooks focused on a single topic or experiment
- Restart kernel and run all cells before committing
- Clear cell outputs before committing (or use tools like `nbstripout`)
- Include requirements at the top of notebooks
- Add conclusions and next steps at the end

### Data Processing

- Write idempotent data processing pipelines
- Validate data at each processing step
- Log data statistics (shape, missing values, distributions)
- Handle missing values explicitly
- Document data transformations

### Testing

- Test data loading and preprocessing functions
- Test model input/output shapes
- Test feature engineering logic
- Use small sample datasets for testing
- Mock external dependencies

## Machine Learning Best Practices

### 1. Reproducibility

- Set random seeds for reproducibility
- Document hardware used (GPU/CPU, memory)
- Record library versions
- Save preprocessing parameters with models
- Use deterministic algorithms when possible

### 2. Data Validation

- Check for data leakage between train/validation/test sets
- Validate data types and ranges
- Monitor data drift in production
- Document data quality issues

### 3. Model Evaluation

- Use appropriate metrics for the problem type
- Implement cross-validation for robust evaluation
- Create baseline models for comparison
- Analyze errors and failure cases
- Consider fairness and bias metrics

### 4. Performance Optimization

- Profile code to identify bottlenecks
- Use vectorized operations (NumPy, Pandas)
- Consider batch processing for large datasets
- Use GPU acceleration when beneficial
- Cache expensive computations

## Common ML Tech Stack

**Expected Libraries** (add to requirements.txt as needed):
```
# Core ML
numpy
pandas
scikit-learn
scipy

# Deep Learning (choose based on need)
tensorflow / pytorch
keras

# Visualization
matplotlib
seaborn
plotly

# Experiment Tracking
mlflow / wandb / tensorboard

# Data Processing
jupyter
notebook
ipykernel

# Utilities
pyyaml
python-dotenv
tqdm
```

## Working with AI Assistants

### What to Expect from AI Help

**AI assistants should:**
- Read existing code before making changes
- Ask about dataset characteristics before suggesting models
- Suggest appropriate evaluation metrics for the task
- Consider computational constraints
- Implement proper train/val/test splits
- Add logging and monitoring code
- Write modular, testable code
- Document hyperparameter choices

**AI assistants should NOT:**
- Commit large data files or model artifacts
- Hardcode file paths or credentials
- Skip data validation steps
- Ignore class imbalance or data quality issues
- Suggest overly complex models without justification
- Make changes without reading existing code first

### Providing Context to AI

When requesting help, provide:
- Dataset description (size, features, target variable)
- Problem type (classification, regression, clustering, etc.)
- Performance requirements or constraints
- Available computational resources
- Current baseline performance
- Specific error messages or issues

## Security and Privacy

- Never commit sensitive data (PII, credentials, API keys)
- Use `.gitignore` for data directories
- Sanitize data before sharing
- Be aware of data licensing and usage rights
- Document data privacy considerations

## File-Specific Guidelines

### README.md
- Should contain project overview, setup instructions, and usage examples
- Update as the project evolves

### .gitignore
Should include:
```
# Data
data/
*.csv
*.parquet
*.h5
*.hdf5

# Models
models/
*.pkl
*.joblib
*.h5
*.pb
*.onnx
*.pth
*.pt
checkpoints/

# Jupyter
.ipynb_checkpoints/
*.ipynb (optionally, or strip outputs)

# Python
__pycache__/
*.py[cod]
*$py.class
*.so
.Python
venv/
env/
.env

# ML specific
mlruns/
wandb/
tensorboard/
.neptune/
```

## Getting Started Checklist

When starting work on this repository:

1. **Environment Setup**
   - [ ] Create virtual environment
   - [ ] Install dependencies from requirements.txt
   - [ ] Set up `.gitignore` if not present
   - [ ] Configure experiment tracking if using

2. **Before Adding Code**
   - [ ] Read existing code and structure
   - [ ] Understand data format and location
   - [ ] Review any existing models or baselines
   - [ ] Check for existing tests

3. **Before Committing**
   - [ ] Run tests if they exist
   - [ ] Clear notebook outputs
   - [ ] Verify no large files or credentials are included
   - [ ] Write descriptive commit message

4. **For New Features**
   - [ ] Create appropriate directory structure
   - [ ] Add configuration files if needed
   - [ ] Write tests for new functionality
   - [ ] Update documentation

## Troubleshooting Common Issues

### Import Errors
- Ensure virtual environment is activated
- Check if package is in requirements.txt
- Verify Python path includes src directory

### Memory Issues
- Use data generators/iterators for large datasets
- Process data in batches
- Use data types efficiently (int8, float32 vs float64)
- Clear unused variables

### Reproducibility Issues
- Set random seeds in NumPy, random, and ML frameworks
- Document exact library versions
- Use deterministic algorithms
- Document hardware differences

## Next Steps for This Repository

**Immediate priorities:**
1. Create basic directory structure
2. Add `.gitignore` for ML projects
3. Create `requirements.txt` with core dependencies
4. Update README.md with project-specific information
5. Set up initial notebook for exploration

**As project grows:**
- Add specific model documentation
- Document dataset characteristics
- Create training and evaluation scripts
- Set up CI/CD for testing
- Add model versioning strategy

---

**Last Updated**: 2026-01-22
**Repository State**: Initialized (minimal structure)
**Python Version**: TBD (specify when set up)
**Primary Contributors**: TBD

---

## Questions or Updates?

This document should evolve with the project. Update it when:
- New conventions are established
- Directory structure changes
- New tools or frameworks are adopted
- Best practices are refined
