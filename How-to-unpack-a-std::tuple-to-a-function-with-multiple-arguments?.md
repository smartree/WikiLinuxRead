How to unpack a std::tuple to match a call function with multiple arguments?

Given the following example:

```cpp
template<typename... Args>
void f(Args... args) {
 ...
}

void t() {
 std::tuple<int, int, double> t;
 // A ordinal way.
 f(std::get<0>(t), std::get<1>(t), std::get<2>(t));
 // But what if a tuple of 4 elements?
 // Is there a generic way to do the job automatically?
 // But how to to match a generic std::tuple<Args...> to f(Args...)?
 // is there a automatic way to do it? See answer below:
 invoke(tuple, index_sequence_for<tuple>);
}

template<typename Tuple, typename size_t...I>
void invoke(const Tuple& args, index_sequence<I...>) {
 f(std::get<I>(args)...);
}
```

The solution is to use the well-known ["indices trick"](http://loungecpp.wikidot.com/tips-and-tricks%3Aindices) — bascally generate a compile-time integer sequence representing the indices of std::tuple, which means (0, std::tuple.size() -1], and use the index to access the elements from the tuple.

1. C++14 has provided [utility templates](http://en.cppreference.com/w/cpp/utility/integer_sequence) (e.g. `make_index_seqence` , `index_sequence_for` ) which helps us do this stuff. 
2. Prior to C++14, we have to implement by our own. Fortunately, the implementation is not complicated, only a few lines of code. In many codebases, they have their own implementation.

LLVM has provided a fully standard implementation:

```cpp
// Represents a compile-time sequence of integers.
// T is the integer type of the sequence, can be size_t, int.
// I is a parameter pack representing the sequence.
template <class T, T... I> struct integer_sequence {
 typedef T value_type;

 static constexpr size_t size() { return sizeof...(I); }
};

// Alias for the common case of a sequence of size_t.
// A pre-defined sequence for common use case.
template <std::size_t... I>
struct index_sequence : integer_sequence<std::size_t, I...> {};

template <std::size_t N, std::size_t... I>
struct build_index_impl : build_index_impl<N - 1, N - 1, I...> {};
template <std::size_t... I>
struct build_index_impl<0, I...> : index_sequence<I...> {};

// Creates a compile-time integer sequence for a parameter pack.
template <class... Ts>
struct index_sequence_for : build_index_impl<sizeof...(Ts)> {};
```

Chromium has provide a simpler implementation of compile-time integer indices:

```cpp
template <size_t... indices>
struct IndicesHolder {};

// Usage: IndicesGenerator<N>::type
template <size_t requested_index, size_t... indices>
struct IndicesGenerator {
 using type = typename IndicesGenerator<requested_index - 1,
 requested_index - 1,
 indices...>::type;
};
template <size_t... indices>
struct IndicesGenerator<0, indices...> {
 using type = IndicesHolder<indices...>;
};
```
