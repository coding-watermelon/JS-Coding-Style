## Legend
☝🏼 = Not discussed yet
👍🏼 = solved

## Redundance for clarification ?

### Sample 1  ☝🏼
Code within a reducer that takes care of form validation. Among others there are two actions, one for validating and another one for invalidating a field.

**With duplication**
```javascript
...
case INVALIDATE_FORM_FIELD:
    return {
      ...state,
      [action.payload.field]: {
        ...state[action.payload.field],
        valid: false,
      },
    };
case VALIDATE_FORM_FIELD:
    return {
      ...state,
      [action.payload.field]: {
        ...state[action.payload.field],
        valid: true,
      },
    };
```

**Without duplication**
```javascript
...
case INVALIDATE_FORM_FIELD:
case VALIDATE_FORM_FIELD:
    return {
      ...state,
      [action.payload.field]: {
        ...state[action.payload.field],
        valid: action.type === VALIDATE_FORM_FIELD,
      },
    };
```
