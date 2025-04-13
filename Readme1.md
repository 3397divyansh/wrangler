# CDAP Wrangler Enhancement - ByteSize and TimeDuration Support

This project extends the CDAP Wrangler library to support parsing and aggregation of `ByteSize` and `TimeDuration` values through a new directive: `aggregate-stats`.

## 🚀 Features Implemented

### ✅ 1. Grammar Extension
- Modified the Wrangler ANTLR grammar to support:
  - `BYTE_SIZE` tokens (e.g., `10MB`, `1.5 GB`)
  - `TIME_DURATION` tokens (e.g., `5s`, `1min`, `2h`)
  
### ✅ 2. Token Handling
- Created new token types in Wrangler:
  - `TokenType.BYTE_SIZE`
  - `TokenType.TIME_DURATION`
- Added `ByteSize.java` and `TimeDuration.java` to handle parsing and conversion:
  - Supports conversions like MB to bytes, seconds to nanoseconds, etc.

### ✅ 3. Recipe Parsing
- Updated `RecipeVisitor.java` to:
  - Parse directives using new token types
  - Instantiate `ByteSize` and `TimeDuration` appropriately

### ✅ 4. Directive: `aggregate-stats`
- Implemented a new directive `AggregateStats.java` that:
  - Aggregates `ByteSize` and `TimeDuration` values from rows
  - Stores results in a transient store and returns a summary row

### ✅ 5. Transient Store Integration
- Used `ExecutorContext.getTransientStore()` to persist intermediate aggregate results

### ✅ 6. Unit Tests (WIP/Planned)
- Plan to test:
  - ByteSize and TimeDuration parsing
  - Recipe parsing with new tokens
  - `aggregate-stats` directive logic

## 📂 Files Modified or Added

- `grammar/Directives.g4`: Added rules for `BYTE_SIZE` and `TIME_DURATION`
- `RecipeVisitor.java`: Parsing logic for new tokens
- `TokenType.java`: Enum additions for new token types
- `ByteSize.java`, `TimeDuration.java`: Parsing logic for new units
- `AggregateStats.java`: New directive for aggregation
- `ExecutorContext.java`, `TransientStore.java`: Ensure `getTransientStore()` is exposed and usable

## 🧪 Example Usage

In a recipe:

```plaintext
aggregate-stats :byteSizeColumn 'file_size' :timeDurationColumn 'duration' :outputByteColumn 'total_size_mb' :outputTimeColumn 'total_duration_sec'
