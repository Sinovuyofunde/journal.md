

## Implement Strategy Pattern in Java (Shipping Cost Calculator)

### Selected Code

Shipping cost calculator (Strategy Pattern opportunity)

---

## 1. The problem statement is:

The original function contains many if-else statements for:

* Different shipping options (standard, express, overnight)
* Different pricing rules per country
* Package size rules

### Issues:

* Hard to read
* Hard to extend
* Bad practice due to multiple conditionals in one function

---

## 2. Selected Pattern: Strategy Pattern

This pattern uses one class per shipping method.

---

## 3. Refactored Code

### Strategy Interface

```javascript
class ShippingStrategy {
  calculate(packageDetails, destinationCountry) {}
}
```

---

### Standard Shipping

```javascript
class StandardShipping extends ShippingStrategy {
  calculate({ weight, length, width, height }, country) {
    let cost;

    if (country === 'USA') cost = weight * 2.5;
    else if (country === 'Canada') cost = weight * 3.5;
    else if (country === 'Mexico') cost = weight * 4.0;
    else cost = weight * 4.5;

    if (weight < 2 && (length * width * height) > 1000) {
      cost += 5;
    }

    return cost;
  }
}
```

---

### Express Shipping

```javascript
class ExpressShipping extends ShippingStrategy {
  calculate({ weight, length, width, height }, country) {
    let cost;

    if (country === 'USA') cost = weight * 4.5;
    else if (country === 'Canada') cost = weight * 5.5;
    else if (country === 'Mexico') cost = weight * 6.0;
    else cost = weight * 7.5;

    if (length * width * height > 5000) {
      cost += 15;
    }

    return cost;
  }
}
```

---

### Overnight Shipping

```javascript
class OvernightShipping extends ShippingStrategy {
  calculate({ weight }, country) {
    if (country === 'USA') return weight * 9.5;
    if (country === 'Canada') return weight * 12.5;

    return "Not available";
  }
}
```

---

### Context Class

```javascript
class ShippingContext {
  constructor(strategy) {
    this.strategy = strategy;
  }

  setStrategy(strategy) {
    this.strategy = strategy;
  }

  calculate(packageDetails, country) {
    return this.strategy.calculate(packageDetails, country);
  }
}
```

---

## 4. Usage

```javascript
const pkg = { weight: 5, length: 10, width: 10, height: 10 };

const context = new ShippingContext(new StandardShipping());
console.log(context.calculate(pkg, 'USA'));

context.setStrategy(new ExpressShipping());
console.log(context.calculate(pkg, 'Canada'));

context.setStrategy(new OvernightShipping());
console.log(context.calculate(pkg, 'USA'));
```

---

## 5. Benefits

* Cleaner code
* Easier to add new shipping methods
* Less if-else logic
* Easier testing of each strategy

---

If you want, I can convert this properly into **Java (real OOP version for submission)** instead of JavaScript.
