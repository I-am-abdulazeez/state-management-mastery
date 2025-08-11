# State Management Mastery

*Master state management in 8 core principles*

[![GitHub stars](https://img.shields.io/github/stars/I-am-abdulazeez/state-management-mastery?style=social)](https://github.com/I-am-abdulazeez/state-management-mastery)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

## 📖 About

State management is the backbone of modern apps. Get it wrong, and you'll spend months debugging "ghost bugs." Get it right, and your app becomes **predictable**, **scalable**, and **maintainable**.

This repository breaks down state management mastery into **8 essential principles** that will transform how you build applications.

## 🎯 The 8 Principles

### 1. **State Management is Your App's Backbone**
Get it wrong, and you'll spend months debugging "ghost bugs" where data appears and disappears mysteriously. Get it right, and your app becomes predictable, scalable, and maintainable.

### 2. **Single Source of Truth**
Every piece of data should have ONE authoritative source. When you duplicate state across components, you're asking for synchronization nightmares. One source, multiple subscribers.

### 3. **Think in Data Flow, Not Components**
Map out how data moves through your app before writing code:
- Where does data originate?
- Who needs to read it? 
- Who can modify it?
- When should updates trigger re-renders?

### 4. **Granular Beats Global**
Instead of one massive global state object, break it into focused, independent chunks. User profile, shopping cart, and app settings shouldn't live in the same state bucket. **Fine-grained reactivity = better performance**.

### 5. **Separate Concerns Clearly**
- **Local state**: Component-specific data (form inputs, toggles)
- **Shared state**: Cross-component data (user auth, theme)
- **Server state**: API responses, cache management

Each has different patterns and tools.

### 6. 🚀 **Choose Tools That Match Your Complexity**

**🟢 Simple apps (Local state, few components):**
- **React**: `useState`, `useReducer`
- **Vue**: `ref()`, `reactive()`

**🟡 Medium complexity (Shared state, multiple features):**
- **React**: Stunk, Zustand, Context API, Effector
- **Vue**: Pinia, Effector

**🔴 Complex apps (Enterprise scale, heavy async):**
- **React**: Stunk, Zustand, RTK, Jotai, Effector
- **Vue**: Pinia + plugins, Effector

**🌐 Framework-agnostic solutions:**
- **Stunk**: Fine-grained reactivity, works with all frameworks
- **Effector**: Works with any UI or server framework. Tested with React, Solid, Vue. (https://github.com/effector/effector)

**💡 Pro tip:** Start simple and migrate up as complexity grows. Don't over-engineer from day one.

### 7. **Debug with Time-Travel**
Good state management should let you:
- See all state changes over time
- Replay actions to reproduce bugs
- Rollback to previous states
- Track which actions caused which updates

**💡Pro Tip: Stunk has inbuilt Time-Travel (`withHistory()`)**

### 8. **Master These Patterns**
When you follow these principles, your apps will have:
- Predictable updates
- Easier debugging
- Better performance
- Simpler testing
- Happier developers

## 🔧 Quick Examples

### Fine-Grained State (Stunk)
```javascript
import { chunk } from "stunk";

const count = chunk(0);

// Get current value
console.log(count.get()); // 0

// Update value
count.set(5);
count.set((prev) => prev + 1); // 6

// Subscribe to changes
count.subscribe((value) => {
  console.log('Count changed:', value);
});

// Reset to initial value
count.reset(); // Back to 0
```

### Computed Values
```javascript
import { chunk, computed } from "stunk";

const price = chunk(100);
const quantity = chunk(2);

// Auto-updates when price or quantity changes
const total = computed(
  [price, quantity],
  (priceValue, quantityValue) => priceValue * quantityValue
);

total.subscribe((value) => {
  console.log('Total:', value); // 200
});

quantity.set(3); // Triggers: "Total: 300"
```

### Data Flow Mapping
```javascript
import { chunk, select } from "stunk";

// ❌ Bad: Duplicated state
let userProfile = { name: 'John', email: 'john@example.com' };
let userName = 'John';
let userEmail = 'john@example.com';

// Synchronization nightmare! Update one, forget the others

// ✅ Good: Single source of truth
const userState = chunk({
  name: 'John',
  email: 'john@example.com',
  avatar: '/avatar.jpg'
});

const userName = select(userState, (state) => state.name);
const userEmail = select(userState, (state) => state.email);

// Subscribe to changes
userName.subscribe((name) => {
  console.log('Name updated:', name);
});

userEmail.subscribe((email) => {
  console.log('Email updated:', email);
});

// Update once, all derived values automatically update
userState.set({ 
  name: 'Jane', 
  email: 'jane@example.com', 
  avatar: '/new-avatar.jpg' 
});
```

## 📚 Related Tools

- **[Stunk](https://github.com/I-am-abdulazeez/stunk)** - Framework-agnostic, fine-grained state management that embodies these principles
- **[Zustand](https://github.com/pmndrs/zustand)** - Lightweight React state management
- **[Pinia](https://github.com/vuejs/pinia)** - Vue's intuitive state management
- **[Effector](https://github.com/effector/effector)** - Meet the new standard for modern TypeScript development. Type safe, reactive, framework agnostic.

## 🤝 Contributing

Found these principles helpful? Contributions welcome:
- Share real-world examples
- Add framework integrations
- Improve documentation
- Report issues

## 📄 License

MIT License - see [LICENSE](./LICENSE) for details.

---

⭐ **Star this repo** if these principles helped you master state management!

*Building better applications through better state management.*
