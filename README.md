// Simple calculator logic
(() => {
  const display = document.getElementById('display');
  const keys = document.querySelector('.keys');

  let expression = '';

  function updateDisplay() {
    display.textContent = expression || '0';
  }

  function appendValue(v) {
    // Prevent multiple dots in a number segment
    if (v === '.') {
      // get last number segment
      const parts = expression.split(/[\+\-\*\/]/);
      const last = parts[parts.length - 1];
      if (last.includes('.')) return;
      if (last === '') {
        // allow leading 0.
        expression += '0';
      }
    }
    expression += v;
    updateDisplay();
  }

  function appendOperator(op) {
    if (expression === '') {
      // allow unary minus
      if (op === '-') {
        expression = '-';
        updateDisplay();
      }
      return;
    }
    // replace trailing operator with new operator
    expression = expression.replace(/[\+\-\*\/]+$/g, '');
    expression += op;
    updateDisplay();
  }

  function clearAll() {
    expression = '';
    updateDisplay();
  }

  function deleteLast() {
    expression = expression.slice(0, -1);
    updateDisplay();
  }

  function evaluateExpression() {
    if (!expression) return;
    // sanitize expression: allow digits, operators, parentheses and dot
    if (!/^[0-9+\-*/().\s]+$/.test(expression)) {
      display.textContent = 'Error';
      expression = '';
      return;
    }
    try {
      // Use Function as a cleaner eval alternative
      // NOTE: This is still evaluating a string; only use trusted input or local use.
      const result = Function('"use strict"; return (' + expression + ')')();
      expression = String(result);
      updateDisplay();
    } catch (e) {
      display.textContent = 'Error';
      expression = '';
    }
  }

  keys.addEventListener('click', (e) => {
    const btn = e.target.closest('button');
    if (!btn) return;

    const action = btn.dataset.action;
    const value = btn.dataset.value;

    if (!action && value) {
      appendValue(value);
      return;
    }

    switch (action) {
      case 'operator':
        appendOperator(value);
        break;
      case 'clear':
        clearAll();
        break;
      case 'delete':
        deleteLast();
        break;
      case 'equals':
        evaluateExpression();
        break;
    }
  });

  // Keyboard support
  window.addEventListener('keydown', (e) => {
    if ((e.key >= '0' && e.key <= '9') || e.key === '.') {
      appendValue(e.key);
      e.preventDefault();
      return;
    }
    if (['+', '-', '*', '/'].includes(e.key)) {
      appendOperator(e.key);
      e.preventDefault();
      return;
    }
    if (e.key === 'Enter' || e.key === '=') {
      evaluateExpression();
      e.preventDefault();
      return;
    }
    if (e.key === 'Backspace') {
      deleteLast();
      e.preventDefault();
      return;
    }
    if (e.key.toLowerCase() === 'c') {
      clearAll();
      e.preventDefault();
      return;
    }
  });

  // initialize
  updateDisplay();// Simple calculator logic
(() => {
  const display = document.getElementById('display');
  const keys = document.querySelector('.keys');

  let expression = '';

  function updateDisplay() {
    display.textContent = expression || '0';
  }

  function appendValue(v) {
    // Prevent multiple dots in a number segment
    if (v === '.') {
      // get last number segment
      const parts = expression.split(/[\+\-\*\/]/);
      const last = parts[parts.length - 1];
      if (last.includes('.')) return;
      if (last === '') {
        // allow leading 0.
        expression += '0';
      }
    }
    expression += v;
    updateDisplay();
  }

  function appendOperator(op) {
    if (expression === '') {
      // allow unary minus
      if (op === '-') {
        expression = '-';
        updateDisplay();
      }
      return;
    }
    // replace trailing operator with new operator
    expression = expression.replace(/[\+\-\*\/]+$/g, '');
    expression += op;
    updateDisplay();
  }

  function clearAll() {
    expression = '';
    updateDisplay();
  }

  function deleteLast() {
    expression = expression.slice(0, -1);
    updateDisplay();
  }

  function evaluateExpression() {
    if (!expression) return;
    // sanitize expression: allow digits, operators, parentheses and dot
    if (!/^[0-9+\-*/().\s]+$/.test(expression)) {
      display.textContent = 'Error';
      expression = '';
      return;
    }
    try {
      // Use Function as a cleaner eval alternative
      // NOTE: This is still evaluating a string; only use trusted input or local use.
      const result = Function('"use strict"; return (' + expression + ')')();
      expression = String(result);
      updateDisplay();
    } catch (e) {
      display.textContent = 'Error';
      expression = '';
    }
  }

  keys.addEventListener('click', (e) => {
    const btn = e.target.closest('button');
    if (!btn) return;

    const action = btn.dataset.action;
    const value = btn.dataset.value;

    if (!action && value) {
      appendValue(value);
      return;
    }

    switch (action) {
      case 'operator':
        appendOperator(value);
        break;
      case 'clear':
        clearAll();
        break;
      case 'delete':
        deleteLast();
        break;
      case 'equals':
        evaluateExpression();
        break;
    }
  });

  // Keyboard support
  window.addEventListener('keydown', (e) => {
    if ((e.key >= '0' && e.key <= '9') || e.key === '.') {
      appendValue(e.key);
      e.preventDefault();
      return;
    }
    if (['+', '-', '*', '/'].includes(e.key)) {
      appendOperator(e.key);
      e.preventDefault();
      return;
    }
    if (e.key === 'Enter' || e.key === '=') {
      evaluateExpression();
      e.preventDefault();
      return;
    }
    if (e.key === 'Backspace') {
      deleteLast();
      e.preventDefault();
      return;
    }
    if (e.key.toLowerCase() === 'c') {
      clearAll();
      e.preventDefault();
      return;
    }
  });

  // initialize
  updateDisplay();
})();
})();
