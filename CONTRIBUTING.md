# Contributing Guidelines

Thank you for your interest in contributing to this research project. While this repository primarily serves as a thesis archive and demonstration of methodologies, contributions that enhance reproducibility, extend experiments, or improve documentation are welcome.

## How to Contribute

### Reporting Issues

If you encounter bugs, have questions about the implementation, or identify areas for improvement:

1. **Search Existing Issues:** Check if your concern has already been raised
2. **Open a New Issue:** Use the GitHub issue tracker with a descriptive title
3. **Provide Context:** Include:
   - Environment details (OS, Python version, GPU specs)
   - Steps to reproduce the problem
   - Expected vs. actual behavior
   - Relevant code snippets or error messages

### Suggesting Enhancements

We welcome suggestions for:

- Additional baseline methods for comparison
- Performance optimizations
- Extended evaluation metrics
- Visualization improvements
- Documentation clarifications

Please open an issue labeled `enhancement` with:
- Clear description of the proposed feature
- Rationale and expected benefits
- Implementation approach (if applicable)

### Code Contributions

#### Development Setup
```bash
# Fork and clone the repository
git clone https://github.com/yourusername/thesis-cloud-removal-crop-mapping.git
cd thesis-cloud-removal-crop-mapping

# Create a feature branch
git checkout -b feature/your-feature-name

# Install development dependencies
pip install -r requirements-dev.txt

# Run tests to verify setup
pytest tests/
```

#### Coding Standards

- **Style:** Follow [PEP 8](https://pep8.org/) for Python code
- **Documentation:** Use NumPy-style docstrings for all functions and classes
- **Type Hints:** Include type annotations for function signatures
- **Testing:** Add unit tests for new functionality (minimum 80% coverage)
- **Commits:** Write clear, atomic commit messages following [Conventional Commits](https://www.conventionalcommits.org/)

Example:
```
feat(preprocessing): add adaptive cloud threshold detection

Implements automatic threshold selection based on scene brightness
distribution to improve cloud masking in heterogeneous landscapes.

Closes #42
```

#### Pull Request Process

1. **Update Documentation:** Ensure `README.md`, docstrings, and relevant markdown files reflect your changes
2. **Add Tests:** Include unit and integration tests covering new code paths
3. **Run Quality Checks:**
```bash
   # Linting
   flake8 src/ tests/
   
   # Type checking
   mypy src/
   
   # Test suite
   pytest tests/ --cov=src --cov-report=html
```
4. **Submit PR:** Provide a clear description linking to relevant issues
5. **Code Review:** Address reviewer feedback promptly and professionally
6. **Merge:** Maintainers will merge approved PRs after final checks

### Research Collaboration

For academic collaborations, dataset sharing, or joint publications:

- **Email:** ramesh.menghwar@example.com
- **Subject Line:** "Research Collaboration - [Topic]"
- **Include:** Your affiliation, research interests, and proposed collaboration scope

## Code of Conduct

### Our Pledge

We are committed to providing a welcoming and inclusive environment for all contributors, regardless of background, identity, or experience level.

### Expected Behavior

- Use respectful and professional language
- Accept constructive criticism gracefully
- Focus on scientific rigor and reproducibility
- Acknowledge contributions of others appropriately
- Prioritize the advancement of knowledge over personal recognition

### Unacceptable Behavior

- Harassment, discrimination, or personal attacks
- Plagiarism or misrepresentation of work
- Deliberate introduction of malicious code
- Spam or off-topic promotional content

### Enforcement

Violations will result in warnings, temporary bans, or permanent exclusion from the project at maintainers' discretion. Report concerns to ramesh.menghwar@example.com.

## Attribution

All significant contributions will be acknowledged in:
- Repository README.md contributors section
- Academic publications (where appropriate)
- Thesis acknowledgments (for major contributions)

Thank you for helping advance open science and reproducible research in remote sensing!

---

**Questions?** Open an issue or contact ramesh.menghwar@example.com
```

---

## **File 3: LICENSE**
```
MIT License

Copyright (c) 2025 Ramesh Kumar Menghwar

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
