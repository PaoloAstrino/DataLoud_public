# 🤝 Contributing Guidelines

Thank you for your interest in contributing to the AI-Powered Document Chatbot! This document provides guidelines and information for contributors.

## 📋 Table of Contents

- [Getting Started](#getting-started)
- [Development Setup](#development-setup)
- [Contribution Types](#contribution-types)
- [Code Guidelines](#code-guidelines)
- [Pull Request Process](#pull-request-process)
- [Issue Reporting](#issue-reporting)
- [Community Guidelines](#community-guidelines)

## 🚀 Getting Started

### Prerequisites

- **Node.js**: Version 18+ for frontend development
- **Python**: Version 3.11+ for backend development
- **Git**: Version control system
- **Code Editor**: VS Code recommended with extensions

### Development Environment

1. **Fork** the repository on GitHub
2. **Clone** your fork locally
3. **Install** dependencies for both frontend and backend
4. **Set up** environment variables
5. **Run** the development servers

## 🛠️ Development Setup

### Frontend Setup (Next.js)

```bash
# Navigate to frontend directory
cd v0-custom-chatbot-interface

# Install dependencies
npm install

# Set up environment variables
cp .env.example .env.local

# Start development server
npm run dev
```

### Backend Setup (Python Flask)

```bash
# Navigate to backend directory
cd ChatBot_v2/chatterbox-document-buddy/backend

# Create virtual environment
python -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate

# Install dependencies
pip install -r requirements.txt

# Set up environment variables
cp .env.example .env

# Start development server
python unified_server.py
```

### Database Setup (Supabase)

1. Create a new Supabase project
2. Run the SQL schema from `supabase_schema.sql`
3. Configure Row Level Security policies
4. Update environment variables with your Supabase credentials

## 🎯 Contribution Types

### 🐛 Bug Fixes

- Fix existing functionality issues
- Improve error handling
- Resolve performance problems
- Address security vulnerabilities

### ✨ New Features

- Add new document processing capabilities
- Enhance AI/ML functionality
- Improve user interface components
- Extend API functionality

### 📚 Documentation

- Update README files
- Add code comments
- Create tutorials and guides
- Improve API documentation

### 🧪 Testing

- Write unit tests
- Add integration tests
- Improve test coverage
- Performance testing

### 🎨 UI/UX Improvements

- Design enhancements
- Accessibility improvements
- Mobile responsiveness
- User experience optimization

## 📝 Code Guidelines

### Frontend (TypeScript/React)

#### Code Style

```typescript
// Use descriptive variable names
const documentProcessingStatus = "processing";

// Prefer functional components with hooks
const ChatInterface: React.FC<ChatProps> = ({ messages, onSendMessage }) => {
  const [inputValue, setInputValue] = useState("");

  // Use proper TypeScript types
  const handleSubmit = (event: React.FormEvent<HTMLFormElement>) => {
    event.preventDefault();
    onSendMessage(inputValue);
    setInputValue("");
  };

  return <form onSubmit={handleSubmit}>{/* Component JSX */}</form>;
};
```

#### Best Practices

- Use TypeScript for type safety
- Follow React hooks guidelines
- Implement proper error boundaries
- Use semantic HTML elements
- Ensure accessibility compliance

### Backend (Python)

#### Code Style

```python
from typing import List, Dict, Optional
import logging

class DocumentProcessor:
    """Process and analyze uploaded documents."""

    def __init__(self, config: Dict[str, str]) -> None:
        self.config = config
        self.logger = logging.getLogger(__name__)

    def process_document(
        self,
        file_path: str,
        chunk_size: int = 1000
    ) -> List[Dict[str, str]]:
        """
        Process document into chunks for analysis.

        Args:
            file_path: Path to the document file
            chunk_size: Maximum size of each chunk

        Returns:
            List of document chunks with metadata

        Raises:
            ProcessingError: If document processing fails
        """
        try:
            # Processing logic here
            return chunks
        except Exception as e:
            self.logger.error(f"Document processing failed: {e}")
            raise ProcessingError(f"Failed to process {file_path}")
```

#### Best Practices

- Use type hints for all functions
- Follow PEP 8 style guidelines
- Include comprehensive docstrings
- Implement proper error handling
- Use logging instead of print statements

### Database (SQL)

#### Schema Guidelines

```sql
-- Use descriptive table and column names
CREATE TABLE chat_sessions (
    id UUID PRIMARY KEY DEFAULT uuid_generate_v4(),
    user_id UUID NOT NULL,
    document_id UUID REFERENCES documents(id) ON DELETE CASCADE,
    created_at TIMESTAMP WITH TIME ZONE DEFAULT NOW(),
    updated_at TIMESTAMP WITH TIME ZONE DEFAULT NOW(),
    session_metadata JSONB DEFAULT '{}'::jsonb,

    -- Add appropriate indexes
    INDEX idx_chat_sessions_user_id (user_id),
    INDEX idx_chat_sessions_document_id (document_id),
    INDEX idx_chat_sessions_created_at (created_at)
);

-- Include Row Level Security
ALTER TABLE chat_sessions ENABLE ROW LEVEL SECURITY;

CREATE POLICY "Users can only access their own sessions"
    ON chat_sessions
    FOR ALL
    USING (user_id = auth.uid());
```

## 🔄 Pull Request Process

### Before Creating a PR

1. **Create an Issue**: Discuss your changes before implementing
2. **Branch Naming**: Use descriptive branch names

   - `feature/add-document-preview`
   - `bugfix/fix-upload-timeout`
   - `docs/update-api-documentation`

3. **Code Quality**: Ensure your code follows project standards
4. **Testing**: Add tests for new functionality
5. **Documentation**: Update relevant documentation

### PR Requirements

#### Checklist

- [ ] Code follows project style guidelines
- [ ] Self-review of the code completed
- [ ] Tests added for new functionality
- [ ] All tests pass locally
- [ ] Documentation updated as needed
- [ ] No merge conflicts with main branch

#### PR Template

```markdown
## Description

Brief description of changes made.

## Type of Change

- [ ] Bug fix
- [ ] New feature
- [ ] Documentation update
- [ ] Performance improvement

## Testing

- [ ] Unit tests added/updated
- [ ] Integration tests added/updated
- [ ] Manual testing completed

## Screenshots (if applicable)

Include screenshots for UI changes.

## Additional Notes

Any additional context or notes for reviewers.
```

### Review Process

1. **Automated Checks**: All CI/CD checks must pass
2. **Code Review**: At least one approved review required
3. **Testing**: Functionality tested in development environment
4. **Documentation**: Updates reviewed for accuracy
5. **Merge**: Squash and merge to main branch

## 🐛 Issue Reporting

### Bug Reports

Use the bug report template:

```markdown
**Bug Description**
A clear description of the bug.

**Steps to Reproduce**

1. Go to '...'
2. Click on '...'
3. Scroll down to '...'
4. See error

**Expected Behavior**
What you expected to happen.

**Actual Behavior**
What actually happened.

**Environment**

- OS: [e.g., Windows 11]
- Browser: [e.g., Chrome 120]
- Version: [e.g., 2.1.0]

**Additional Context**
Screenshots, logs, or other relevant information.
```

### Feature Requests

Use the feature request template:

```markdown
**Feature Description**
Clear description of the requested feature.

**Problem Statement**
What problem does this feature solve?

**Proposed Solution**
How would you like this feature to work?

**Alternative Solutions**
Alternative approaches you've considered.

**Additional Context**
Mockups, examples, or related issues.
```

## 👥 Community Guidelines

### Code of Conduct

We are committed to providing a welcoming and inclusive environment:

- **Be Respectful**: Treat all contributors with respect
- **Be Inclusive**: Welcome newcomers and diverse perspectives
- **Be Constructive**: Provide helpful feedback and suggestions
- **Be Professional**: Maintain professional communication

### Communication Channels

- **GitHub Issues**: Bug reports and feature requests
- **GitHub Discussions**: General questions and discussions
- **Pull Request Reviews**: Code-related discussions
- **Documentation**: Updates and improvements

### Recognition

Contributors are recognized through:

- **Contributor List**: Listed in project documentation
- **Commit Attribution**: Proper commit attribution
- **Release Notes**: Contributions mentioned in changelog
- **Community Highlights**: Featured contributions

## 🧪 Testing Guidelines

### Frontend Testing

```typescript
// Example Jest test
import { render, screen, fireEvent } from "@testing-library/react";
import ChatInterface from "../components/ChatInterface";

describe("ChatInterface", () => {
  test("sends message when form is submitted", () => {
    const mockSendMessage = jest.fn();
    render(<ChatInterface onSendMessage={mockSendMessage} />);

    const input = screen.getByRole("textbox");
    const button = screen.getByRole("button", { name: /send/i });

    fireEvent.change(input, { target: { value: "Test message" } });
    fireEvent.click(button);

    expect(mockSendMessage).toHaveBeenCalledWith("Test message");
  });
});
```

### Backend Testing

```python
import pytest
from unittest.mock import Mock, patch
from app.services.document_processor import DocumentProcessor

class TestDocumentProcessor:
    def setup_method(self):
        self.processor = DocumentProcessor({'api_key': 'test_key'})

    @patch('app.services.document_processor.extract_text')
    def test_process_document_success(self, mock_extract):
        mock_extract.return_value = "Sample document text"

        result = self.processor.process_document('test.pdf')

        assert len(result) > 0
        assert result[0]['content'] == "Sample document text"
```

## 📊 Performance Guidelines

### Frontend Performance

- Use React.memo for expensive components
- Implement proper loading states
- Optimize bundle size with code splitting
- Use efficient state management

### Backend Performance

- Implement proper caching strategies
- Use async/await for I/O operations
- Optimize database queries
- Monitor memory usage

### Database Performance

- Use appropriate indexes
- Optimize query performance
- Monitor connection pooling
- Regular performance analysis

## 🔒 Security Considerations

### Security Checklist

- [ ] Input validation and sanitization
- [ ] SQL injection prevention
- [ ] XSS protection
- [ ] CSRF token implementation
- [ ] Secure authentication
- [ ] Environment variable protection

### Reporting Security Issues

Please report security vulnerabilities privately:

1. **Email**: security@project-domain.com
2. **Encrypted Communication**: Use provided PGP key
3. **Responsible Disclosure**: Allow time for fixes before public disclosure

Thank you for contributing to the AI-Powered Document Chatbot! 🚀
