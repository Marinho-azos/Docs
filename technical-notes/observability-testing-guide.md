# Observability Testing Pattern Guide

## 🎯 **Overview**

This guide provides a standardized pattern for testing observability implementations across projects. It ensures comprehensive coverage of span creation, error handling, and graceful degradation scenarios.

## 📋 **Core Testing Principles**

### 1. **Mock External Dependencies**
- Use standard `@patch` decorators when dependencies are available in test environment
- Mock at the module level only when dependencies are unavailable
- Use proper type hints and specifications

### 2. **Test Both Happy Path and Edge Cases**
- Active span scenarios
- No active span scenarios (graceful degradation)
- Various data types and edge cases

### 3. **Verify Actual Calls**
- Don't just test that methods don't crash
- Verify the exact calls made to the underlying library
- Check parameter values and call sequences

## 🏗️ **Test Structure Pattern**

### **File Organization**
```
tests/
├── unit/
│   └── frameworks/
│       └── observability/
│           └── test_observability_service.py
```

### **Test Class Structure**
```python
class TestObservabilityManager:
    """Test suite for ObservabilityManager."""
    
    def setup_method(self) -> None:
        """Set up test fixtures for each test."""
        # Initialize your observability manager
        # Create mock objects
    
    # Group tests by method being tested
    # Use descriptive test names that explain the scenario
```

## 🧪 **Required Test Categories**

### **1. Span Creation Tests**

#### **Basic Functionality**
- ✅ `test_set_span_with_active_span` - Normal operation
- ✅ `test_set_span_with_no_active_span` - Graceful degradation

#### **Data Type Coverage**
- ✅ `test_set_span_with_different_data_types` - Various data types
- ✅ `test_set_span_with_empty_string_key` - Edge case handling
- ✅ `test_set_span_with_unicode_characters` - International support

#### **Multiple Operations**
- ✅ `test_multiple_set_span_calls` - Sequential operations

### **2. Error Handling Tests**

#### **Basic Error Scenarios**
- ✅ `test_set_span_error_with_active_span` - Normal error handling
- ✅ `test_set_span_error_with_no_active_span` - Graceful degradation

#### **Exception Type Coverage**
- ✅ `test_set_span_error_with_different_exception_types` - Various exceptions
- ✅ `test_set_span_error_with_exception_without_message` - Empty messages
- ✅ `test_set_span_error_with_exception_with_complex_message` - Special characters

### **3. Integration Tests**
- ✅ `test_set_span_and_set_span_error_sequence` - Combined operations
- ✅ `test_observability_manager_implements_interface` - Contract compliance

## 🔧 **Implementation Template**

### **Step 1: Clean Imports (When Dependencies Available)**
```python
from unittest.mock import MagicMock, call, patch

from adapters.interfaces.observability_service import ObservabilityService
from frameworks.observability import ObservabilityManager
```

### **Step 2: Test Class Setup with Type Annotations**
```python
class TestObservabilityManager:
    """Test suite for ObservabilityManager."""

    def setup_method(self) -> None:
        """Set up test fixtures."""
        self.observability_manager = ObservabilityManager()
        self.mock_span = MagicMock()
```

### **Step 3: Basic Test Pattern with Proper Types**
```python
@patch("your_project.observability.manager.tracer")
def test_set_span_with_active_span(self, mock_tracer: MagicMock) -> None:
    """Test set_span when there's an active span."""
    # Arrange
    mock_tracer.current_span.return_value = self.mock_span
    key = "test_key"
    value = "test_value"

    # Act
    self.observability_manager.set_span(key, value)

    # Assert
    mock_tracer.current_span.assert_called_once()
    self.mock_span.set_tag.assert_called_once_with(key, value)
```

## 📊 **Test Data Patterns**

### **Data Type Test Cases**
```python
test_cases = [
    ("string", "hello"),
    ("integer", 42),
    ("float", 3.14),
    ("boolean", True),
    ("list", [1, 2, 3]),
    ("dict", {"key": "value"}),
    ("none", None),
]
```

### **Exception Type Test Cases**
```python
test_cases = [
    (ValueError("Value error"), "ValueError"),
    (TypeError("Type error"), "TypeError"),
    (RuntimeError("Runtime error"), "RuntimeError"),
    (KeyError("Key error"), "KeyError"),
    (IndexError("Index error"), "IndexError"),
]
```

### **Edge Case Test Cases**
```python
edge_cases = [
    ("empty_string", ""),
    ("unicode_key", "user_name_émojis"),
    ("unicode_value", "José 🚀"),
    ("special_chars", "Error: !@#$%^&*()_+-=[]{}|;':\",./<>?"),
]
```

## 🎯 **Assertion Patterns**

### **Single Call Verification**
```python
mock_tracer.current_span.assert_called_once()
self.mock_span.set_tag.assert_called_once_with(key, value)
```

### **Multiple Call Verification**
```python
self.mock_span.set_tag.assert_has_calls([
    call("key1", "value1"),
    call("key2", "value2"),
    call("key3", "value3")
])
```

### **Error State Verification**
```python
assert self.mock_span.error == 1
self.mock_span.set_tag.assert_has_calls([
    call("error", True),
    call("error.type", "ValueError"),
    call("error.message", "Invalid input")
])
```

### **No-Call Verification**
```python
mock_tracer.current_span.assert_called_once()
self.mock_span.set_tag.assert_not_called()
```

## 🔄 **Mock Reset Pattern**

For tests with multiple iterations:
```python
for test_case in test_cases:
    # Reset mock for each test case
    self.mock_span.reset_mock()
    
    # Run your test
    self.observability_manager.method(test_case)
    
    # Verify results
    self.mock_span.set_tag.assert_called_with(expected_args)
```

## 📝 **Test Naming Convention**

### **Pattern**: `test_{method_name}_with_{scenario}`

**Examples**:
- `test_set_span_with_active_span`
- `test_set_span_with_no_active_span`
- `test_set_span_error_with_different_exception_types`
- `test_multiple_set_span_calls`

## 🚀 **Coverage Requirements**

### **Minimum Coverage Targets**
- **Line Coverage**: 100%
- **Branch Coverage**: 100%
- **Method Coverage**: 100%

### **Coverage Verification**
```bash
# Run tests with coverage
pytest tests/unit/observability/ --cov=src/observability --cov-report=term-missing

# Ensure 100% coverage
pytest tests/unit/observability/ --cov=src/observability --cov-fail-under=100
```

## 🔍 **Quality Checklist**

### **Before Submitting Tests**
- [ ] All happy path scenarios covered
- [ ] All error scenarios covered
- [ ] Edge cases tested (empty strings, unicode, special chars)
- [ ] Graceful degradation verified (no active span)
- [ ] Multiple operation sequences tested
- [ ] Interface compliance verified
- [ ] 100% code coverage achieved
- [ ] All tests pass consistently
- [ ] **All type annotations properly added** ✅
- [ ] **Mock setup is clean and isolated** ✅
- [ ] Test names are descriptive and follow convention

## 🎨 **Customization Guidelines**

### **For Different Observability Libraries**

**OpenTelemetry**:
```python
# Replace ddtrace with opentelemetry
@patch("your_project.observability.manager.tracer")
def test_method(self, mock_tracer: MagicMock) -> None:
    # Test logic
```

**Jaeger**:
```python
# Replace ddtrace with jaeger_client
@patch("your_project.observability.manager.tracer")
def test_method(self, mock_tracer: MagicMock) -> None:
    # Test logic
```

### **For Different Methods**

Adapt the test patterns for your specific observability interface:
- `set_tag` → `add_attribute`
- `set_span_error` → `record_exception`
- `current_span` → `get_current_span`

## 🚨 **Fallback Mocking (When Dependencies Unavailable)**

### **Module-Level Mocking (Use Only When Necessary)**
```python
import sys
from types import ModuleType
from unittest.mock import MagicMock, call, patch

# Mock observability library before importing your manager
# Replace 'ddtrace' with your observability library
mock_observability_lib = ModuleType('ddtrace')
mock_tracer = MagicMock()
mock_observability_lib.tracer = mock_tracer
sys.modules['ddtrace'] = mock_observability_lib

from your_project.observability import ObservabilityManager  # noqa: E402
```

**When to Use This Approach**:
- External dependency not available in test environment
- Import-time failures that can't be resolved with standard mocking
- Legacy systems with complex import dependencies

**When NOT to Use This Approach**:
- Dependencies are available in test environment (use standard `@patch`)
- Simple method-level mocking is sufficient
- You want clean, maintainable test code

## 📚 **Additional Resources**

### **Best Practices**
1. **Isolation**: Each test should be independent
2. **Clarity**: Test names should explain the scenario
3. **Completeness**: Cover all code paths and edge cases
4. **Maintainability**: Use patterns and avoid duplication
5. **Performance**: Tests should run quickly
6. **Type Safety**: Always include proper type annotations

### **Common Pitfalls to Avoid**
- ❌ Not mocking external dependencies
- ❌ Testing implementation details instead of behavior
- ❌ Incomplete edge case coverage
- ❌ Not verifying actual calls to underlying library
- ❌ Ignoring graceful degradation scenarios
- ❌ Missing type annotations (causes mypy errors)
- ❌ Complex module-level mocking when simple patching works

---

## 🎯 **Summary**

This pattern ensures your observability layer is:
- **Reliable**: Comprehensive test coverage catches regressions
- **Robust**: Edge cases and error scenarios are handled
- **Maintainable**: Consistent patterns across projects
- **Type-Safe**: Proper type annotations prevent runtime errors
- **Production-Ready**: Verified behavior under all conditions

### **Key Updates in This Version**
- ✅ **Simplified approach** when dependencies are available
- ✅ **Type annotation requirements** for all test methods
- ✅ **Fallback mocking strategy** for unavailable dependencies
- ✅ **Clean, maintainable test structure** using standard patterns
- ✅ **100% coverage requirements** with proper verification

Follow this guide for every observability implementation to maintain consistent quality and reliability across all your projects.
