# unit-5-wdf

# Unit V - React Library II: Comprehensive Overview

**Key Findings Summary**
This unit explores advanced React concepts crucial for building scalable applications. Custom Hooks enable logic reuse, while HTTP clients like Fetch/Axios handle data fetching. Behavior Subjects manage state reactively, and component patterns (Stateful/Stateless) optimize UI architecture. Error handling, testing, and tools like React Native/StoryBook round out modern development workflows.

---

## Custom Hooks: Encapsulating Logic Reusability

### Definition and Purpose

Custom Hooks are JavaScript functions prefixed with `use` that leverage React’s built-in Hooks (e.g., `useState`, `useEffect`) to share stateful logic across components[^2]. They adhere to Hook rules (e.g., no conditional calls) and simplify complex workflows like data fetching or subscriptions[^2][^7].

### Implementation Example

```javascript
import { useState, useEffect } from 'react';

function useWindowWidth() {
  const [width, setWidth] = useState(window.innerWidth);
  useEffect(() =&gt; {
    const handleResize = () =&gt; setWidth(window.innerWidth);
    window.addEventListener('resize', handleResize);
    return () =&gt; window.removeEventListener('resize', handleResize);
  }, []);
  return width;
}
```

This Hook tracks window width changes, demonstrating state management and cleanup[^2].

### Best Practices

1. **Naming Convention**: Always prefix with `use` (e.g., `useFetch`)[^2].
2. **Reusability**: Extract logic common across components (e.g., form validation)[^2].
3. **Testing**: Isolate Hook behavior using testing libraries[^7].

---

## HTTP Requests: Fetch vs. Axios

### Fetch API

- **Native Browser API**: No installation required, supports promises[^6].
- **Manual Parsing**: Requires explicit `.json()` calls and error checks[^5][^6].

```javascript
fetch('https://api.example.com/data')
  .then(response =&gt; {
    if (!response.ok) throw new Error('Network error');
    return response.json();
  })
  .catch(error =&gt; console.error(error));
```


### Axios Library

- **Third-Party Features**: Automatic JSON parsing, interceptors, and broader browser support[^6].
- **Simplified Syntax**:

```javascript
axios.get('https://api.example.com/data')
  .then(response =&gt; console.log(response.data))
  .catch(error =&gt; console.error(error));
```


#### Comparison Table

| Feature | Fetch | Axios |
| :-- | :-- | :-- |
| Installation | Native | `npm install axios` |
| Error Handling | Manual | Built-in |
| Request Cancellation | AbortController | CancelToken |
| Interceptors | No | Yes |


---

## Services and Behavior Subjects

### Service Architecture

Services encapsulate business logic (e.g., API calls) and use React Context for state sharing[^4].

```javascript
// dataService.js  
export const fetchData = async (url) =&gt; {
  try {
    const response = await fetch(url);
    return response.json();
  } catch (error) {
    console.error('Fetch error:', error);
  }
};
```


### Behavior Subjects (RxJS)

- **Reactive State Management**: Emits current value to new subscribers[^3][^7].
- **Initialization**:

```javascript
const currentLanguage$ = new BehaviorSubject('en-gb');
currentLanguage$.next('fr'); // Update value  
currentLanguage$.subscribe(lang =&gt; updateUI(lang)); // React to changes[^8]  
```


---

## Component Patterns: Stateful vs. Stateless

### Stateless Components

- **Role**: Presentational; receive data via props, no internal state.
- **Example**:

```javascript
const UserList = ({ users }) =&gt; (
  <ul>{users.map(user =&gt; <li>{user.name}</li>)}</ul>
);
```


### Stateful Components

- **Role**: Manage state/logic, pass data to stateless children.
- **Example**:

```javascript
class UserDashboard extends React.Component {
  state = { users: [] };
  componentDidMount() { fetchUsers().then(users =&gt; this.setState({ users })); }
  render() { return &lt;UserList users={this.state.users} /&gt;; }
}
```


### Container Components

- **Purpose**: Mediate data flow between stateful and presentational components.
- **Use Case**: Connecting Redux stores to UI elements.

---

## Error Handling and CORS

### Strategies

1. **Try/Catch Blocks**: Wrap async operations[^5].
2. **Error Boundaries**: Fallback UI for component errors.
3. **CORS Configuration**: Set headers on the server (e.g., `Access-Control-Allow-Origin`)[^5].

### Build and Environment Variables

- **Environment-Specific Configs**: Use `.env` files for API endpoints[^7].

```ini
REACT_APP_API_URL=https://api.prod.example.com
```


---

## Testing with React Testing Library

### Key Practices

- **Render Components**: Simulate user interactions.
- **Assertions**: Validate DOM outcomes.

```javascript
test('displays loading state', () =&gt; {
  render(&lt;DataFetchingComponent /&gt;);
  expect(screen.getByText('Loading...')).toBeInTheDocument();
});
```


---

## React Native and Storybook

### React Native Basics

- **Cross-Platform Apps**: Reuse React skills for mobile development.
- **Core Components**: `&lt;View&gt;`, `&lt;Text&gt;`, `&lt;Button&gt;`.


### Storybook Integration

- **Component Isolation**: Develop/test UI components independently.
- **Setup**:

```bash
npx storybook init
```

- **Usage**: Create `.stories.js` files for visual testing.

---

## Conclusion and Exam Preparation Tips

1. **Focus Areas**: Custom Hooks, HTTP clients, component patterns.
2. **Practice**: Implement a CRUD app using Fetch/Axios and Behavior Subjects.
3. **Revision**: Revisit testing workflows and React Native setup steps.

**Recommended Study Flow**

- Morning: Custom Hooks and HTTP libraries.
- Afternoon: State management, error handling.
- Evening: Mock tests using React Testing Library.

By methodically addressing each topic and leveraging code examples, this unit equips developers to build robust, maintainable React applications[^2][^4][^7].

<div style="text-align: center">⁂</div>

[^1]: https://ppl-ai-file-upload.s3.amazonaws.com/web/direct-files/attachments/66614433/196016c0-5f43-4a75-95df-1f2c88e8d407/WDF_Unit_5.pdf

[^2]: https://dev.to/hasancse/mastering-custom-hooks-in-react-a-comprehensive-guide-1bfb

[^3]: https://xgrommx.github.io/rx-book/content/subjects/behavior_subject/index.html

[^4]: https://www.hackemist.com/react-service-pattern

[^5]: https://www.restack.io/p/building-ai-focused-websites-with-react-answer-react-fetch-api-call-example-cat-ai

[^6]: https://apidog.com/articles/react-fetch-vs-axios/

[^7]: https://www.linkedin.com/pulse/angular-using-behaviorsubject-react-user-action-stefanos-kouroupis

[^8]: https://dev.to/sidramaqbool/understanding-stateful-and-stateless-components-in-react-22oo

[^9]: https://javascriptpatterns.vercel.app/patterns/react-patterns/conpres

[^10]: https://blog.logrocket.com/react-error-handling-react-error-boundary/

[^11]: https://dev.to/nagakumar_reddy_316f25396/understanding-cors-a-crucial-security-feature-for-your-react-applications-1fpk

[^12]: https://www.codecademy.com/learn/learn-react-testing/modules/react-testing-library/cheatsheet

[^13]: https://dev.to/syakirurahman/react-custom-hooks-best-practices-with-example-usecases-4e2l

[^14]: https://pub.dev/documentation/find_dropdown/latest/rxdart_behavior_subject/BehaviorSubject-class.html

[^15]: https://www.linkedin.com/pulse/essential-design-patterns-every-react-developer-must-know-karl-cereno-um56e

[^16]: https://dev.to/rahulvijayvergiya/fetch-vs-axios-key-differences-and-use-cases-jd5

[^17]: https://dev.to/delia_code/building-custom-hooks-in-react-best-practices-and-use-cases-273l

[^18]: https://react.dev/learn/reusing-logic-with-custom-hooks

[^19]: https://legacy.reactjs.org/docs/hooks-custom.html

[^20]: https://www.youtube.com/watch?v=I2Bgi0Qcdvc

[^21]: https://blog.stackademic.com/react-fetch-api-d478146e6367?gi=87eade741667

[^22]: https://dev.to/hasancse/best-practices-for-creating-reusable-custom-hooks-in-react-37nj

[^23]: https://github.com/josebalius/use-behavior-subject

[^24]: https://www.angularminds.com/blog/react-architecture-patterns-in-reactjs-apps

[^25]: https://reactnative.dev/docs/network

[^26]: https://medium.com/@jenscript/harnessing-react-custom-hooks-a-new-strategy-for-organizing-logic-67bdb6252a7d

[^27]: https://www.linkedin.com/pulse/angular-using-behaviorsubject-react-user-action-stefanos-kouroupis

[^28]: https://aglowiditsolutions.com/blog/react-architectural-patterns/

[^29]: https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API/Using_Fetch

[^30]: https://blog.logrocket.com/axios-vs-fetch-best-http-requests/

[^31]: https://www.reddit.com/r/learnjavascript/comments/ymv7ex/why_do_people_use_axios_instead_of_fetch/

[^32]: https://blog.logrocket.com/axios-vs-fetch-2025/

[^33]: https://blog.devops.dev/getting-started-with-react-native-a-comprehensive-guide-for-beginners-444518b4119e?gi=7b6a9977eb94

[^34]: https://dev.to/kpiteng/axios-vs-fetch-1eh5

[^35]: https://softchris.github.io/books/rxjs/behavior-subject/

[^36]: https://insightfultscript.com/collections/programming/react/react-statefull-stateless/

[^37]: https://www.linkedin.com/pulse/container-presentational-pattern-react-abhishek-bohora

[^38]: https://builtin.com/software-engineering-perspectives/react-error-boundary

[^39]: https://www.delftstack.com/howto/react/react-cors/

[^40]: https://expertbeacon.com/react-testing-library-a-comprehensive-tutorial-with-code-examples/

[^41]: https://codezup.com/react-native-tutorial-for-beginners/

