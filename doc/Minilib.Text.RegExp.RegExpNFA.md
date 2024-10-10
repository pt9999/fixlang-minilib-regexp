# `module Minilib.Text.RegExp.RegExpNFA`

NFA (Nondeterministic Finite Automaton). This is internal module of `RegExp`.

For details, see web pages below.
- https://swtch.com/~rsc/regexp/regexp1.html
- https://zenn.dev/canalun/articles/regexp_and_automaton

# Types and aliases

## `namespace Minilib.Text.RegExp.RegExpNFA`

### `type Group = (Std::I64, Std::I64)`

Type of a matched group.
The group is represented as two stream positions: `(begin, end)`.
`-1` means that the stream position is undefined.

### `type Groups = Std::Array Minilib.Text.RegExp.RegExpNFA::Group`

Type of the array of matched groups.

### `type NFA = unbox struct { ...fields... }`

NFA

#### field `nodes : Std::Array Minilib.Text.RegExp.RegExpNFA::NFANode`

#### field `initial_node : Minilib.Text.RegExp.RegExpNFA::NodeID`

#### field `accepting_node : Minilib.Text.RegExp.RegExpNFA::NodeID`

#### field `group_count : Std::I64`

#### field `quant_count : Std::I64`

#### field `debug : Std::Bool`

### `type NFAExecutor = unbox struct { ...fields... }`

The NFA executor

#### field `stream : Minilib.Text.SimpleParser::Stream::Stream`

#### field `nfa : Minilib.Text.RegExp.RegExpNFA::NFA`

#### field `empty_state_set : Minilib.Text.RegExp.RegExpNFA::NFAStateSet`

#### field `state_set : Minilib.Text.RegExp.RegExpNFA::NFAStateSet`

#### field `stack : Std::Iterator Minilib.Text.RegExp.RegExpNFA::NFAState`

#### field `accepted_states : Minilib.Text.RegExp.RegExpNFA::NFAStateSet`

### `type NFAFrag = unbox struct { ...fields... }`

NFA Fragment

NFA Fragment is a collection of nodes. It exports one input,
And a function to set the output.
Internally, the output of a fragment is a collection of outputs of one or more nodes.
Calling `set_output()` will change them all.

#### field `input : Minilib.Text.RegExp.RegExpNFA::NodeID`

#### field `set_output : Minilib.Text.RegExp.RegExpNFA::NodeID -> Minilib.Text.RegExp.RegExpNFA::NFA -> Minilib.Text.RegExp.RegExpNFA::NFA`

#### field `label : Std::String`

### `type NFANode = unbox struct { ...fields... }`

NFA node

NFA node has one input (ID of this node) and three outputs
(one output guarded by the action, and two outputs with no guard).

#### field `id : Minilib.Text.RegExp.RegExpNFA::NodeID`

#### field `action : Minilib.Text.RegExp.RegExpNFA::NFANodeAction`

#### field `output_on_action : Minilib.Text.RegExp.RegExpNFA::NodeID`

#### field `output : Minilib.Text.RegExp.RegExpNFA::NodeID`

#### field `output2 : Minilib.Text.RegExp.RegExpNFA::NodeID`

#### field `label : Std::String`

### `type NFANodeAction = unbox union { ...variants... }`

Actions that has to be performed before the state makes a transition to `node.@out_on_action`.

#### variant `sa_none : ()`

#### variant `sa_char_match : Minilib.Text.RegExp.RegExpPattern::CharClass`

#### variant `sa_assert : Minilib.Text.RegExp.RegExpPattern::PAssertion`

#### variant `sa_group_begin : Std::I64`

#### variant `sa_group_end : Std::I64`

#### variant `sa_quant_begin : Std::I64`

#### variant `sa_quant_loop : Std::I64`

#### variant `sa_quant_end : (Std::I64, Std::I64, Std::I64)`

### `type NFAState = unbox struct { ...fields... }`

NFA state

#### field `id : Minilib.Text.RegExp.RegExpNFA::NodeID`

#### field `groups : Std::Array (Std::I64, Std::I64)`

#### field `quants : Std::Array Std::I64`

### `type NFAStateSet = unbox struct { ...fields... }`

NFA state set, used for NFA state transition

#### field `array : Std::Array Minilib.Text.RegExp.RegExpNFA::NFAState`

#### field `map : HashMap::HashMap Minilib.Text.RegExp.RegExpNFA::NFAState Std::Bool`

### `type NodeID = unbox struct { ...fields... }`

ID of NFA node. -1 is invalid value.

#### field `val : Std::I64`

### `type QuantID = Std::I64`

Type of special quantifiers ID.
Special quantifiers are quantifieres other than `X?` `X*` `X+`.
In other words, they are `X{n}` `X{n,}` `X{n,m}` etc.
Special quantifiers are hard to implement only using node transition,
so its iteration count are stored in the NFA state, and managed by `sa_quant_*` actions.

### `type ReplaceFrag = unbox union { ...variants... }`

A replacement fragment

#### variant `rep_literal : Std::U8`

#### variant `rep_group : Std::I64`

# Traits and aliases

# Trait implementations

### `impl Minilib.Text.RegExp.RegExpNFA::NFA : Std::ToString`

### `impl Minilib.Text.RegExp.RegExpNFA::NFANode : Std::ToString`

### `impl Minilib.Text.RegExp.RegExpNFA::NFANodeAction : Std::ToString`

### `impl Minilib.Text.RegExp.RegExpNFA::NFAState : Hash::Hash`

### `impl Minilib.Text.RegExp.RegExpNFA::NFAState : Std::Eq`

### `impl Minilib.Text.RegExp.RegExpNFA::NFAState : Std::ToString`

### `impl Minilib.Text.RegExp.RegExpNFA::NodeID : Hash::Hash`

### `impl Minilib.Text.RegExp.RegExpNFA::NodeID : Std::Eq`

### `impl Minilib.Text.RegExp.RegExpNFA::NodeID : Std::ToString`

# Values

## `namespace Minilib.Text.RegExp.RegExpNFA::NFA`

### `@accepting_node : Minilib.Text.RegExp.RegExpNFA::NFA -> Minilib.Text.RegExp.RegExpNFA::NodeID`

Retrieves the field `accepting_node` from a value of `NFA`.

### `@debug : Minilib.Text.RegExp.RegExpNFA::NFA -> Std::Bool`

Retrieves the field `debug` from a value of `NFA`.

### `@group_count : Minilib.Text.RegExp.RegExpNFA::NFA -> Std::I64`

Retrieves the field `group_count` from a value of `NFA`.

### `@initial_node : Minilib.Text.RegExp.RegExpNFA::NFA -> Minilib.Text.RegExp.RegExpNFA::NodeID`

Retrieves the field `initial_node` from a value of `NFA`.

### `@nodes : Minilib.Text.RegExp.RegExpNFA::NFA -> Std::Array Minilib.Text.RegExp.RegExpNFA::NFANode`

Retrieves the field `nodes` from a value of `NFA`.

### `@quant_count : Minilib.Text.RegExp.RegExpNFA::NFA -> Std::I64`

Retrieves the field `quant_count` from a value of `NFA`.

### `act_accepting_node : [f : Std::Functor] (Minilib.Text.RegExp.RegExpNFA::NodeID -> f Minilib.Text.RegExp.RegExpNFA::NodeID) -> Minilib.Text.RegExp.RegExpNFA::NFA -> f Minilib.Text.RegExp.RegExpNFA::NFA`

Updates a value of `NFA` by applying a functorial action to field `accepting_node`.

### `act_debug : [f : Std::Functor] (Std::Bool -> f Std::Bool) -> Minilib.Text.RegExp.RegExpNFA::NFA -> f Minilib.Text.RegExp.RegExpNFA::NFA`

Updates a value of `NFA` by applying a functorial action to field `debug`.

### `act_group_count : [f : Std::Functor] (Std::I64 -> f Std::I64) -> Minilib.Text.RegExp.RegExpNFA::NFA -> f Minilib.Text.RegExp.RegExpNFA::NFA`

Updates a value of `NFA` by applying a functorial action to field `group_count`.

### `act_initial_node : [f : Std::Functor] (Minilib.Text.RegExp.RegExpNFA::NodeID -> f Minilib.Text.RegExp.RegExpNFA::NodeID) -> Minilib.Text.RegExp.RegExpNFA::NFA -> f Minilib.Text.RegExp.RegExpNFA::NFA`

Updates a value of `NFA` by applying a functorial action to field `initial_node`.

### `act_nodes : [f : Std::Functor] (Std::Array Minilib.Text.RegExp.RegExpNFA::NFANode -> f (Std::Array Minilib.Text.RegExp.RegExpNFA::NFANode)) -> Minilib.Text.RegExp.RegExpNFA::NFA -> f Minilib.Text.RegExp.RegExpNFA::NFA`

Updates a value of `NFA` by applying a functorial action to field `nodes`.

### `act_quant_count : [f : Std::Functor] (Std::I64 -> f Std::I64) -> Minilib.Text.RegExp.RegExpNFA::NFA -> f Minilib.Text.RegExp.RegExpNFA::NFA`

Updates a value of `NFA` by applying a functorial action to field `quant_count`.

### `compile : Minilib.Text.RegExp.RegExpPattern::Pattern -> Minilib.Text.RegExp.RegExpNFA::NFA`

`NFA::compile(pattern)` compiles a pattern to NFA.

### `debug : Std::String -> Minilib.Text.RegExp.RegExpNFA::NFA -> ()`

### `empty : Minilib.Text.RegExp.RegExpNFA::NFA`

An empty NFA.

### `execute : Std::String -> Minilib.Text.RegExp.RegExpNFA::NFA -> Minilib.Text.RegExp.RegExpNFA::NFAExecutor`

`nfa.execute(target)` executes matching.

### `get_node : Minilib.Text.RegExp.RegExpNFA::NodeID -> Minilib.Text.RegExp.RegExpNFA::NFA -> Minilib.Text.RegExp.RegExpNFA::NFANode`

`nfa.get_node(id)` gets the node whose @id is `id`.

### `mod_accepting_node : (Minilib.Text.RegExp.RegExpNFA::NodeID -> Minilib.Text.RegExp.RegExpNFA::NodeID) -> Minilib.Text.RegExp.RegExpNFA::NFA -> Minilib.Text.RegExp.RegExpNFA::NFA`

Updates a value of `NFA` by applying a function to field `accepting_node`.

### `mod_debug : (Std::Bool -> Std::Bool) -> Minilib.Text.RegExp.RegExpNFA::NFA -> Minilib.Text.RegExp.RegExpNFA::NFA`

Updates a value of `NFA` by applying a function to field `debug`.

### `mod_group_count : (Std::I64 -> Std::I64) -> Minilib.Text.RegExp.RegExpNFA::NFA -> Minilib.Text.RegExp.RegExpNFA::NFA`

Updates a value of `NFA` by applying a function to field `group_count`.

### `mod_initial_node : (Minilib.Text.RegExp.RegExpNFA::NodeID -> Minilib.Text.RegExp.RegExpNFA::NodeID) -> Minilib.Text.RegExp.RegExpNFA::NFA -> Minilib.Text.RegExp.RegExpNFA::NFA`

Updates a value of `NFA` by applying a function to field `initial_node`.

### `mod_node : Minilib.Text.RegExp.RegExpNFA::NodeID -> (Minilib.Text.RegExp.RegExpNFA::NFANode -> Minilib.Text.RegExp.RegExpNFA::NFANode) -> Minilib.Text.RegExp.RegExpNFA::NFA -> Minilib.Text.RegExp.RegExpNFA::NFA`

`nfa.mod_node(id, f)` modifies the node whose @id is `id`.

### `mod_nodes : (Std::Array Minilib.Text.RegExp.RegExpNFA::NFANode -> Std::Array Minilib.Text.RegExp.RegExpNFA::NFANode) -> Minilib.Text.RegExp.RegExpNFA::NFA -> Minilib.Text.RegExp.RegExpNFA::NFA`

Updates a value of `NFA` by applying a function to field `nodes`.

### `mod_quant_count : (Std::I64 -> Std::I64) -> Minilib.Text.RegExp.RegExpNFA::NFA -> Minilib.Text.RegExp.RegExpNFA::NFA`

Updates a value of `NFA` by applying a function to field `quant_count`.

### `new_node : Minilib.Text.RegExp.RegExpNFA::NFA -> (Minilib.Text.RegExp.RegExpNFA::NFA, Minilib.Text.RegExp.RegExpNFA::NodeID)`

Creates new node. Returns the new node id.

### `new_quant : Minilib.Text.RegExp.RegExpNFA::NFA -> (Minilib.Text.RegExp.RegExpNFA::NFA, Std::I64)`

Creates new quant. Returns the new quant id.

### `set_accepting_node : Minilib.Text.RegExp.RegExpNFA::NodeID -> Minilib.Text.RegExp.RegExpNFA::NFA -> Minilib.Text.RegExp.RegExpNFA::NFA`

Updates a value of `NFA` by setting field `accepting_node` to a specified one.

### `set_debug : Std::Bool -> Minilib.Text.RegExp.RegExpNFA::NFA -> Minilib.Text.RegExp.RegExpNFA::NFA`

Updates a value of `NFA` by setting field `debug` to a specified one.

### `set_frag_output : Minilib.Text.RegExp.RegExpNFA::NFAFrag -> Minilib.Text.RegExp.RegExpNFA::NodeID -> Minilib.Text.RegExp.RegExpNFA::NFA -> Minilib.Text.RegExp.RegExpNFA::NFA`

`nfa.set_frag_output(frag, out)` sets the output of the fragment to `out`.

### `set_group_count : Std::I64 -> Minilib.Text.RegExp.RegExpNFA::NFA -> Minilib.Text.RegExp.RegExpNFA::NFA`

Updates a value of `NFA` by setting field `group_count` to a specified one.

### `set_initial_node : Minilib.Text.RegExp.RegExpNFA::NodeID -> Minilib.Text.RegExp.RegExpNFA::NFA -> Minilib.Text.RegExp.RegExpNFA::NFA`

Updates a value of `NFA` by setting field `initial_node` to a specified one.

### `set_nodes : Std::Array Minilib.Text.RegExp.RegExpNFA::NFANode -> Minilib.Text.RegExp.RegExpNFA::NFA -> Minilib.Text.RegExp.RegExpNFA::NFA`

Updates a value of `NFA` by setting field `nodes` to a specified one.

### `set_quant_count : Std::I64 -> Minilib.Text.RegExp.RegExpNFA::NFA -> Minilib.Text.RegExp.RegExpNFA::NFA`

Updates a value of `NFA` by setting field `quant_count` to a specified one.

## `namespace Minilib.Text.RegExp.RegExpNFA::NFAExecutor`

### `@accepted_states : Minilib.Text.RegExp.RegExpNFA::NFAExecutor -> Minilib.Text.RegExp.RegExpNFA::NFAStateSet`

Retrieves the field `accepted_states` from a value of `NFAExecutor`.

### `@empty_state_set : Minilib.Text.RegExp.RegExpNFA::NFAExecutor -> Minilib.Text.RegExp.RegExpNFA::NFAStateSet`

Retrieves the field `empty_state_set` from a value of `NFAExecutor`.

### `@nfa : Minilib.Text.RegExp.RegExpNFA::NFAExecutor -> Minilib.Text.RegExp.RegExpNFA::NFA`

Retrieves the field `nfa` from a value of `NFAExecutor`.

### `@stack : Minilib.Text.RegExp.RegExpNFA::NFAExecutor -> Std::Iterator Minilib.Text.RegExp.RegExpNFA::NFAState`

Retrieves the field `stack` from a value of `NFAExecutor`.

### `@state_set : Minilib.Text.RegExp.RegExpNFA::NFAExecutor -> Minilib.Text.RegExp.RegExpNFA::NFAStateSet`

Retrieves the field `state_set` from a value of `NFAExecutor`.

### `@stream : Minilib.Text.RegExp.RegExpNFA::NFAExecutor -> Minilib.Text.SimpleParser::Stream::Stream`

Retrieves the field `stream` from a value of `NFAExecutor`.

### `_add_to_state_set_and_stack : Minilib.Text.RegExp.RegExpNFA::NFAState -> Minilib.Text.RegExp.RegExpNFA::NFAExecutor -> Minilib.Text.RegExp.RegExpNFA::NFAExecutor`

Adds a state to the state set if not added yet, then pushes the state to the stack.

### `_check_for_accepting_state : Minilib.Text.RegExp.RegExpNFA::NFAExecutor -> Minilib.Text.RegExp.RegExpNFA::NFAExecutor`

Checks for accepting state

### `_pop_stack : Minilib.Text.RegExp.RegExpNFA::NFAExecutor -> Std::Option (Minilib.Text.RegExp.RegExpNFA::NFAState, Minilib.Text.RegExp.RegExpNFA::NFAExecutor)`

### `_transition_on_action : Minilib.Text.RegExp.RegExpNFA::NFANode -> Minilib.Text.RegExp.RegExpNFA::NFAState -> Minilib.Text.RegExp.RegExpNFA::NFAExecutor -> Minilib.Text.RegExp.RegExpNFA::NFAExecutor`

Applies transitions on an action with empty string.

### `_transition_with_char : Std::U8 -> Minilib.Text.RegExp.RegExpNFA::NFAExecutor -> Minilib.Text.RegExp.RegExpNFA::NFAExecutor`

Applies transitions with a string of one character.

### `_transition_with_empty_string : Minilib.Text.RegExp.RegExpNFA::NFAExecutor -> Minilib.Text.RegExp.RegExpNFA::NFAExecutor`

Applies transitions with an empty string.

### `act_accepted_states : [f : Std::Functor] (Minilib.Text.RegExp.RegExpNFA::NFAStateSet -> f Minilib.Text.RegExp.RegExpNFA::NFAStateSet) -> Minilib.Text.RegExp.RegExpNFA::NFAExecutor -> f Minilib.Text.RegExp.RegExpNFA::NFAExecutor`

Updates a value of `NFAExecutor` by applying a functorial action to field `accepted_states`.

### `act_empty_state_set : [f : Std::Functor] (Minilib.Text.RegExp.RegExpNFA::NFAStateSet -> f Minilib.Text.RegExp.RegExpNFA::NFAStateSet) -> Minilib.Text.RegExp.RegExpNFA::NFAExecutor -> f Minilib.Text.RegExp.RegExpNFA::NFAExecutor`

Updates a value of `NFAExecutor` by applying a functorial action to field `empty_state_set`.

### `act_nfa : [f : Std::Functor] (Minilib.Text.RegExp.RegExpNFA::NFA -> f Minilib.Text.RegExp.RegExpNFA::NFA) -> Minilib.Text.RegExp.RegExpNFA::NFAExecutor -> f Minilib.Text.RegExp.RegExpNFA::NFAExecutor`

Updates a value of `NFAExecutor` by applying a functorial action to field `nfa`.

### `act_stack : [f : Std::Functor] (Std::Iterator Minilib.Text.RegExp.RegExpNFA::NFAState -> f (Std::Iterator Minilib.Text.RegExp.RegExpNFA::NFAState)) -> Minilib.Text.RegExp.RegExpNFA::NFAExecutor -> f Minilib.Text.RegExp.RegExpNFA::NFAExecutor`

Updates a value of `NFAExecutor` by applying a functorial action to field `stack`.

### `act_state_set : [f : Std::Functor] (Minilib.Text.RegExp.RegExpNFA::NFAStateSet -> f Minilib.Text.RegExp.RegExpNFA::NFAStateSet) -> Minilib.Text.RegExp.RegExpNFA::NFAExecutor -> f Minilib.Text.RegExp.RegExpNFA::NFAExecutor`

Updates a value of `NFAExecutor` by applying a functorial action to field `state_set`.

### `act_stream : [f : Std::Functor] (Minilib.Text.SimpleParser::Stream::Stream -> f Minilib.Text.SimpleParser::Stream::Stream) -> Minilib.Text.RegExp.RegExpNFA::NFAExecutor -> f Minilib.Text.RegExp.RegExpNFA::NFAExecutor`

Updates a value of `NFAExecutor` by applying a functorial action to field `stream`.

### `execute : Minilib.Text.RegExp.RegExpNFA::NFAExecutor -> Minilib.Text.RegExp.RegExpNFA::NFAExecutor`

Make transitions until end of stream is reached, or the state set becomes empty.

### `make : Minilib.Text.SimpleParser::Stream::Stream -> Minilib.Text.RegExp.RegExpNFA::NFA -> Minilib.Text.RegExp.RegExpNFA::NFAExecutor`

Creates an executor.

### `mod_accepted_states : (Minilib.Text.RegExp.RegExpNFA::NFAStateSet -> Minilib.Text.RegExp.RegExpNFA::NFAStateSet) -> Minilib.Text.RegExp.RegExpNFA::NFAExecutor -> Minilib.Text.RegExp.RegExpNFA::NFAExecutor`

Updates a value of `NFAExecutor` by applying a function to field `accepted_states`.

### `mod_empty_state_set : (Minilib.Text.RegExp.RegExpNFA::NFAStateSet -> Minilib.Text.RegExp.RegExpNFA::NFAStateSet) -> Minilib.Text.RegExp.RegExpNFA::NFAExecutor -> Minilib.Text.RegExp.RegExpNFA::NFAExecutor`

Updates a value of `NFAExecutor` by applying a function to field `empty_state_set`.

### `mod_nfa : (Minilib.Text.RegExp.RegExpNFA::NFA -> Minilib.Text.RegExp.RegExpNFA::NFA) -> Minilib.Text.RegExp.RegExpNFA::NFAExecutor -> Minilib.Text.RegExp.RegExpNFA::NFAExecutor`

Updates a value of `NFAExecutor` by applying a function to field `nfa`.

### `mod_stack : (Std::Iterator Minilib.Text.RegExp.RegExpNFA::NFAState -> Std::Iterator Minilib.Text.RegExp.RegExpNFA::NFAState) -> Minilib.Text.RegExp.RegExpNFA::NFAExecutor -> Minilib.Text.RegExp.RegExpNFA::NFAExecutor`

Updates a value of `NFAExecutor` by applying a function to field `stack`.

### `mod_state_set : (Minilib.Text.RegExp.RegExpNFA::NFAStateSet -> Minilib.Text.RegExp.RegExpNFA::NFAStateSet) -> Minilib.Text.RegExp.RegExpNFA::NFAExecutor -> Minilib.Text.RegExp.RegExpNFA::NFAExecutor`

Updates a value of `NFAExecutor` by applying a function to field `state_set`.

### `mod_stream : (Minilib.Text.SimpleParser::Stream::Stream -> Minilib.Text.SimpleParser::Stream::Stream) -> Minilib.Text.RegExp.RegExpNFA::NFAExecutor -> Minilib.Text.RegExp.RegExpNFA::NFAExecutor`

Updates a value of `NFAExecutor` by applying a function to field `stream`.

### `set_accepted_states : Minilib.Text.RegExp.RegExpNFA::NFAStateSet -> Minilib.Text.RegExp.RegExpNFA::NFAExecutor -> Minilib.Text.RegExp.RegExpNFA::NFAExecutor`

Updates a value of `NFAExecutor` by setting field `accepted_states` to a specified one.

### `set_empty_state_set : Minilib.Text.RegExp.RegExpNFA::NFAStateSet -> Minilib.Text.RegExp.RegExpNFA::NFAExecutor -> Minilib.Text.RegExp.RegExpNFA::NFAExecutor`

Updates a value of `NFAExecutor` by setting field `empty_state_set` to a specified one.

### `set_nfa : Minilib.Text.RegExp.RegExpNFA::NFA -> Minilib.Text.RegExp.RegExpNFA::NFAExecutor -> Minilib.Text.RegExp.RegExpNFA::NFAExecutor`

Updates a value of `NFAExecutor` by setting field `nfa` to a specified one.

### `set_stack : Std::Iterator Minilib.Text.RegExp.RegExpNFA::NFAState -> Minilib.Text.RegExp.RegExpNFA::NFAExecutor -> Minilib.Text.RegExp.RegExpNFA::NFAExecutor`

Updates a value of `NFAExecutor` by setting field `stack` to a specified one.

### `set_state_set : Minilib.Text.RegExp.RegExpNFA::NFAStateSet -> Minilib.Text.RegExp.RegExpNFA::NFAExecutor -> Minilib.Text.RegExp.RegExpNFA::NFAExecutor`

Updates a value of `NFAExecutor` by setting field `state_set` to a specified one.

### `set_stream : Minilib.Text.SimpleParser::Stream::Stream -> Minilib.Text.RegExp.RegExpNFA::NFAExecutor -> Minilib.Text.RegExp.RegExpNFA::NFAExecutor`

Updates a value of `NFAExecutor` by setting field `stream` to a specified one.

## `namespace Minilib.Text.RegExp.RegExpNFA::NFAFrag`

### `@input : Minilib.Text.RegExp.RegExpNFA::NFAFrag -> Minilib.Text.RegExp.RegExpNFA::NodeID`

Retrieves the field `input` from a value of `NFAFrag`.

### `@label : Minilib.Text.RegExp.RegExpNFA::NFAFrag -> Std::String`

Retrieves the field `label` from a value of `NFAFrag`.

### `@set_output : Minilib.Text.RegExp.RegExpNFA::NFAFrag -> Minilib.Text.RegExp.RegExpNFA::NodeID -> Minilib.Text.RegExp.RegExpNFA::NFA -> Minilib.Text.RegExp.RegExpNFA::NFA`

Retrieves the field `set_output` from a value of `NFAFrag`.

### `_compile_action : Minilib.Text.RegExp.RegExpNFA::NFANodeAction -> Minilib.Text.RegExp.RegExpNFA::NFA -> (Minilib.Text.RegExp.RegExpNFA::NFA, Minilib.Text.RegExp.RegExpNFA::NFAFrag)`

Compiles an action to a fragment.

### `_compile_either : Minilib.Text.RegExp.RegExpNFA::NFAFrag -> Minilib.Text.RegExp.RegExpNFA::NFAFrag -> Minilib.Text.RegExp.RegExpNFA::NFA -> (Minilib.Text.RegExp.RegExpNFA::NFA, Minilib.Text.RegExp.RegExpNFA::NFAFrag)`

Compiles an alternative of two fragments (`e1|e2`) to a fragment.

### `_compile_null_sequence : Minilib.Text.RegExp.RegExpNFA::NFA -> (Minilib.Text.RegExp.RegExpNFA::NFA, Minilib.Text.RegExp.RegExpNFA::NFAFrag)`

Compiles null sequence (``) to a fragment.

### `_compile_one_or_more : Minilib.Text.RegExp.RegExpNFA::NFAFrag -> Minilib.Text.RegExp.RegExpNFA::NFA -> (Minilib.Text.RegExp.RegExpNFA::NFA, Minilib.Text.RegExp.RegExpNFA::NFAFrag)`

Compiles one or more occurrence (`e+`) to a fragment.

### `_compile_seq : Minilib.Text.RegExp.RegExpNFA::NFAFrag -> Minilib.Text.RegExp.RegExpNFA::NFAFrag -> Minilib.Text.RegExp.RegExpNFA::NFA -> (Minilib.Text.RegExp.RegExpNFA::NFA, Minilib.Text.RegExp.RegExpNFA::NFAFrag)`

Compiles a sequence of two fragments (`e1 e2`) to a fragment.

### `_compile_special_quant : Minilib.Text.RegExp.RegExpNFA::NFAFrag -> Std::I64 -> Std::I64 -> Minilib.Text.RegExp.RegExpNFA::NFA -> (Minilib.Text.RegExp.RegExpNFA::NFA, Minilib.Text.RegExp.RegExpNFA::NFAFrag)`

Compiles special quant (`e{min,max}`) to a fragment.

### `_compile_zero_or_more : Minilib.Text.RegExp.RegExpNFA::NFAFrag -> Minilib.Text.RegExp.RegExpNFA::NFA -> (Minilib.Text.RegExp.RegExpNFA::NFA, Minilib.Text.RegExp.RegExpNFA::NFAFrag)`

Compiles zero or more occurrence (`e*`) to a fragment.

### `_compile_zero_or_once : Minilib.Text.RegExp.RegExpNFA::NFAFrag -> Minilib.Text.RegExp.RegExpNFA::NFA -> (Minilib.Text.RegExp.RegExpNFA::NFA, Minilib.Text.RegExp.RegExpNFA::NFAFrag)`

Compiles zero or once occurrence (`e?`) to a fragment.

### `act_input : [f : Std::Functor] (Minilib.Text.RegExp.RegExpNFA::NodeID -> f Minilib.Text.RegExp.RegExpNFA::NodeID) -> Minilib.Text.RegExp.RegExpNFA::NFAFrag -> f Minilib.Text.RegExp.RegExpNFA::NFAFrag`

Updates a value of `NFAFrag` by applying a functorial action to field `input`.

### `act_label : [f : Std::Functor] (Std::String -> f Std::String) -> Minilib.Text.RegExp.RegExpNFA::NFAFrag -> f Minilib.Text.RegExp.RegExpNFA::NFAFrag`

Updates a value of `NFAFrag` by applying a functorial action to field `label`.

### `act_set_output : [f : Std::Functor] ((Minilib.Text.RegExp.RegExpNFA::NodeID -> Minilib.Text.RegExp.RegExpNFA::NFA -> Minilib.Text.RegExp.RegExpNFA::NFA) -> f (Minilib.Text.RegExp.RegExpNFA::NodeID -> Minilib.Text.RegExp.RegExpNFA::NFA -> Minilib.Text.RegExp.RegExpNFA::NFA)) -> Minilib.Text.RegExp.RegExpNFA::NFAFrag -> f Minilib.Text.RegExp.RegExpNFA::NFAFrag`

Updates a value of `NFAFrag` by applying a functorial action to field `set_output`.

### `compile_pattern : Minilib.Text.RegExp.RegExpPattern::Pattern -> Minilib.Text.RegExp.RegExpNFA::NFA -> (Minilib.Text.RegExp.RegExpNFA::NFA, Minilib.Text.RegExp.RegExpNFA::NFAFrag)`

`nfa.compile_pattern(pattern)` compiles a pattern to a fragment.

### `mod_input : (Minilib.Text.RegExp.RegExpNFA::NodeID -> Minilib.Text.RegExp.RegExpNFA::NodeID) -> Minilib.Text.RegExp.RegExpNFA::NFAFrag -> Minilib.Text.RegExp.RegExpNFA::NFAFrag`

Updates a value of `NFAFrag` by applying a function to field `input`.

### `mod_label : (Std::String -> Std::String) -> Minilib.Text.RegExp.RegExpNFA::NFAFrag -> Minilib.Text.RegExp.RegExpNFA::NFAFrag`

Updates a value of `NFAFrag` by applying a function to field `label`.

### `mod_set_output : ((Minilib.Text.RegExp.RegExpNFA::NodeID -> Minilib.Text.RegExp.RegExpNFA::NFA -> Minilib.Text.RegExp.RegExpNFA::NFA) -> Minilib.Text.RegExp.RegExpNFA::NodeID -> Minilib.Text.RegExp.RegExpNFA::NFA -> Minilib.Text.RegExp.RegExpNFA::NFA) -> Minilib.Text.RegExp.RegExpNFA::NFAFrag -> Minilib.Text.RegExp.RegExpNFA::NFAFrag`

Updates a value of `NFAFrag` by applying a function to field `set_output`.

### `set_input : Minilib.Text.RegExp.RegExpNFA::NodeID -> Minilib.Text.RegExp.RegExpNFA::NFAFrag -> Minilib.Text.RegExp.RegExpNFA::NFAFrag`

Updates a value of `NFAFrag` by setting field `input` to a specified one.

### `set_label : Std::String -> Minilib.Text.RegExp.RegExpNFA::NFAFrag -> Minilib.Text.RegExp.RegExpNFA::NFAFrag`

Updates a value of `NFAFrag` by setting field `label` to a specified one.

### `set_set_output : (Minilib.Text.RegExp.RegExpNFA::NodeID -> Minilib.Text.RegExp.RegExpNFA::NFA -> Minilib.Text.RegExp.RegExpNFA::NFA) -> Minilib.Text.RegExp.RegExpNFA::NFAFrag -> Minilib.Text.RegExp.RegExpNFA::NFAFrag`

Updates a value of `NFAFrag` by setting field `set_output` to a specified one.

## `namespace Minilib.Text.RegExp.RegExpNFA::NFANode`

### `@action : Minilib.Text.RegExp.RegExpNFA::NFANode -> Minilib.Text.RegExp.RegExpNFA::NFANodeAction`

Retrieves the field `action` from a value of `NFANode`.

### `@id : Minilib.Text.RegExp.RegExpNFA::NFANode -> Minilib.Text.RegExp.RegExpNFA::NodeID`

Retrieves the field `id` from a value of `NFANode`.

### `@label : Minilib.Text.RegExp.RegExpNFA::NFANode -> Std::String`

Retrieves the field `label` from a value of `NFANode`.

### `@output : Minilib.Text.RegExp.RegExpNFA::NFANode -> Minilib.Text.RegExp.RegExpNFA::NodeID`

Retrieves the field `output` from a value of `NFANode`.

### `@output2 : Minilib.Text.RegExp.RegExpNFA::NFANode -> Minilib.Text.RegExp.RegExpNFA::NodeID`

Retrieves the field `output2` from a value of `NFANode`.

### `@output_on_action : Minilib.Text.RegExp.RegExpNFA::NFANode -> Minilib.Text.RegExp.RegExpNFA::NodeID`

Retrieves the field `output_on_action` from a value of `NFANode`.

### `_INVALID_NODE_ID : Minilib.Text.RegExp.RegExpNFA::NodeID`

An invalid node ID.

### `act_action : [f : Std::Functor] (Minilib.Text.RegExp.RegExpNFA::NFANodeAction -> f Minilib.Text.RegExp.RegExpNFA::NFANodeAction) -> Minilib.Text.RegExp.RegExpNFA::NFANode -> f Minilib.Text.RegExp.RegExpNFA::NFANode`

Updates a value of `NFANode` by applying a functorial action to field `action`.

### `act_id : [f : Std::Functor] (Minilib.Text.RegExp.RegExpNFA::NodeID -> f Minilib.Text.RegExp.RegExpNFA::NodeID) -> Minilib.Text.RegExp.RegExpNFA::NFANode -> f Minilib.Text.RegExp.RegExpNFA::NFANode`

Updates a value of `NFANode` by applying a functorial action to field `id`.

### `act_label : [f : Std::Functor] (Std::String -> f Std::String) -> Minilib.Text.RegExp.RegExpNFA::NFANode -> f Minilib.Text.RegExp.RegExpNFA::NFANode`

Updates a value of `NFANode` by applying a functorial action to field `label`.

### `act_output : [f : Std::Functor] (Minilib.Text.RegExp.RegExpNFA::NodeID -> f Minilib.Text.RegExp.RegExpNFA::NodeID) -> Minilib.Text.RegExp.RegExpNFA::NFANode -> f Minilib.Text.RegExp.RegExpNFA::NFANode`

Updates a value of `NFANode` by applying a functorial action to field `output`.

### `act_output2 : [f : Std::Functor] (Minilib.Text.RegExp.RegExpNFA::NodeID -> f Minilib.Text.RegExp.RegExpNFA::NodeID) -> Minilib.Text.RegExp.RegExpNFA::NFANode -> f Minilib.Text.RegExp.RegExpNFA::NFANode`

Updates a value of `NFANode` by applying a functorial action to field `output2`.

### `act_output_on_action : [f : Std::Functor] (Minilib.Text.RegExp.RegExpNFA::NodeID -> f Minilib.Text.RegExp.RegExpNFA::NodeID) -> Minilib.Text.RegExp.RegExpNFA::NFANode -> f Minilib.Text.RegExp.RegExpNFA::NFANode`

Updates a value of `NFANode` by applying a functorial action to field `output_on_action`.

### `empty : Minilib.Text.RegExp.RegExpNFA::NFANode`

An empty node

### `mod_action : (Minilib.Text.RegExp.RegExpNFA::NFANodeAction -> Minilib.Text.RegExp.RegExpNFA::NFANodeAction) -> Minilib.Text.RegExp.RegExpNFA::NFANode -> Minilib.Text.RegExp.RegExpNFA::NFANode`

Updates a value of `NFANode` by applying a function to field `action`.

### `mod_id : (Minilib.Text.RegExp.RegExpNFA::NodeID -> Minilib.Text.RegExp.RegExpNFA::NodeID) -> Minilib.Text.RegExp.RegExpNFA::NFANode -> Minilib.Text.RegExp.RegExpNFA::NFANode`

Updates a value of `NFANode` by applying a function to field `id`.

### `mod_label : (Std::String -> Std::String) -> Minilib.Text.RegExp.RegExpNFA::NFANode -> Minilib.Text.RegExp.RegExpNFA::NFANode`

Updates a value of `NFANode` by applying a function to field `label`.

### `mod_output : (Minilib.Text.RegExp.RegExpNFA::NodeID -> Minilib.Text.RegExp.RegExpNFA::NodeID) -> Minilib.Text.RegExp.RegExpNFA::NFANode -> Minilib.Text.RegExp.RegExpNFA::NFANode`

Updates a value of `NFANode` by applying a function to field `output`.

### `mod_output2 : (Minilib.Text.RegExp.RegExpNFA::NodeID -> Minilib.Text.RegExp.RegExpNFA::NodeID) -> Minilib.Text.RegExp.RegExpNFA::NFANode -> Minilib.Text.RegExp.RegExpNFA::NFANode`

Updates a value of `NFANode` by applying a function to field `output2`.

### `mod_output_on_action : (Minilib.Text.RegExp.RegExpNFA::NodeID -> Minilib.Text.RegExp.RegExpNFA::NodeID) -> Minilib.Text.RegExp.RegExpNFA::NFANode -> Minilib.Text.RegExp.RegExpNFA::NFANode`

Updates a value of `NFANode` by applying a function to field `output_on_action`.

### `set_action : Minilib.Text.RegExp.RegExpNFA::NFANodeAction -> Minilib.Text.RegExp.RegExpNFA::NFANode -> Minilib.Text.RegExp.RegExpNFA::NFANode`

Updates a value of `NFANode` by setting field `action` to a specified one.

### `set_id : Minilib.Text.RegExp.RegExpNFA::NodeID -> Minilib.Text.RegExp.RegExpNFA::NFANode -> Minilib.Text.RegExp.RegExpNFA::NFANode`

Updates a value of `NFANode` by setting field `id` to a specified one.

### `set_label : Std::String -> Minilib.Text.RegExp.RegExpNFA::NFANode -> Minilib.Text.RegExp.RegExpNFA::NFANode`

Updates a value of `NFANode` by setting field `label` to a specified one.

### `set_output : Minilib.Text.RegExp.RegExpNFA::NodeID -> Minilib.Text.RegExp.RegExpNFA::NFANode -> Minilib.Text.RegExp.RegExpNFA::NFANode`

Updates a value of `NFANode` by setting field `output` to a specified one.

### `set_output2 : Minilib.Text.RegExp.RegExpNFA::NodeID -> Minilib.Text.RegExp.RegExpNFA::NFANode -> Minilib.Text.RegExp.RegExpNFA::NFANode`

Updates a value of `NFANode` by setting field `output2` to a specified one.

### `set_output_on_action : Minilib.Text.RegExp.RegExpNFA::NodeID -> Minilib.Text.RegExp.RegExpNFA::NFANode -> Minilib.Text.RegExp.RegExpNFA::NFANode`

Updates a value of `NFANode` by setting field `output_on_action` to a specified one.

## `namespace Minilib.Text.RegExp.RegExpNFA::NFANodeAction`

### `as_sa_assert : Minilib.Text.RegExp.RegExpNFA::NFANodeAction -> Minilib.Text.RegExp.RegExpPattern::PAssertion`

Unwraps a union value of `NFANodeAction` as the variant `sa_assert`.
If the value is not the variant `sa_assert`, this function aborts the program.

### `as_sa_char_match : Minilib.Text.RegExp.RegExpNFA::NFANodeAction -> Minilib.Text.RegExp.RegExpPattern::CharClass`

Unwraps a union value of `NFANodeAction` as the variant `sa_char_match`.
If the value is not the variant `sa_char_match`, this function aborts the program.

### `as_sa_group_begin : Minilib.Text.RegExp.RegExpNFA::NFANodeAction -> Std::I64`

Unwraps a union value of `NFANodeAction` as the variant `sa_group_begin`.
If the value is not the variant `sa_group_begin`, this function aborts the program.

### `as_sa_group_end : Minilib.Text.RegExp.RegExpNFA::NFANodeAction -> Std::I64`

Unwraps a union value of `NFANodeAction` as the variant `sa_group_end`.
If the value is not the variant `sa_group_end`, this function aborts the program.

### `as_sa_none : Minilib.Text.RegExp.RegExpNFA::NFANodeAction -> ()`

Unwraps a union value of `NFANodeAction` as the variant `sa_none`.
If the value is not the variant `sa_none`, this function aborts the program.

### `as_sa_quant_begin : Minilib.Text.RegExp.RegExpNFA::NFANodeAction -> Std::I64`

Unwraps a union value of `NFANodeAction` as the variant `sa_quant_begin`.
If the value is not the variant `sa_quant_begin`, this function aborts the program.

### `as_sa_quant_end : Minilib.Text.RegExp.RegExpNFA::NFANodeAction -> (Std::I64, Std::I64, Std::I64)`

Unwraps a union value of `NFANodeAction` as the variant `sa_quant_end`.
If the value is not the variant `sa_quant_end`, this function aborts the program.

### `as_sa_quant_loop : Minilib.Text.RegExp.RegExpNFA::NFANodeAction -> Std::I64`

Unwraps a union value of `NFANodeAction` as the variant `sa_quant_loop`.
If the value is not the variant `sa_quant_loop`, this function aborts the program.

### `is_sa_assert : Minilib.Text.RegExp.RegExpNFA::NFANodeAction -> Std::Bool`

Checks if a union value of `NFANodeAction` is the variant `sa_assert`.

### `is_sa_char_match : Minilib.Text.RegExp.RegExpNFA::NFANodeAction -> Std::Bool`

Checks if a union value of `NFANodeAction` is the variant `sa_char_match`.

### `is_sa_group_begin : Minilib.Text.RegExp.RegExpNFA::NFANodeAction -> Std::Bool`

Checks if a union value of `NFANodeAction` is the variant `sa_group_begin`.

### `is_sa_group_end : Minilib.Text.RegExp.RegExpNFA::NFANodeAction -> Std::Bool`

Checks if a union value of `NFANodeAction` is the variant `sa_group_end`.

### `is_sa_none : Minilib.Text.RegExp.RegExpNFA::NFANodeAction -> Std::Bool`

Checks if a union value of `NFANodeAction` is the variant `sa_none`.

### `is_sa_quant_begin : Minilib.Text.RegExp.RegExpNFA::NFANodeAction -> Std::Bool`

Checks if a union value of `NFANodeAction` is the variant `sa_quant_begin`.

### `is_sa_quant_end : Minilib.Text.RegExp.RegExpNFA::NFANodeAction -> Std::Bool`

Checks if a union value of `NFANodeAction` is the variant `sa_quant_end`.

### `is_sa_quant_loop : Minilib.Text.RegExp.RegExpNFA::NFANodeAction -> Std::Bool`

Checks if a union value of `NFANodeAction` is the variant `sa_quant_loop`.

### `mod_sa_assert : (Minilib.Text.RegExp.RegExpPattern::PAssertion -> Minilib.Text.RegExp.RegExpPattern::PAssertion) -> Minilib.Text.RegExp.RegExpNFA::NFANodeAction -> Minilib.Text.RegExp.RegExpNFA::NFANodeAction`

Updates a value of union `NFANodeAction` by applying a function if it is the variant `sa_assert`, or doing nothing otherwise.

### `mod_sa_char_match : (Minilib.Text.RegExp.RegExpPattern::CharClass -> Minilib.Text.RegExp.RegExpPattern::CharClass) -> Minilib.Text.RegExp.RegExpNFA::NFANodeAction -> Minilib.Text.RegExp.RegExpNFA::NFANodeAction`

Updates a value of union `NFANodeAction` by applying a function if it is the variant `sa_char_match`, or doing nothing otherwise.

### `mod_sa_group_begin : (Std::I64 -> Std::I64) -> Minilib.Text.RegExp.RegExpNFA::NFANodeAction -> Minilib.Text.RegExp.RegExpNFA::NFANodeAction`

Updates a value of union `NFANodeAction` by applying a function if it is the variant `sa_group_begin`, or doing nothing otherwise.

### `mod_sa_group_end : (Std::I64 -> Std::I64) -> Minilib.Text.RegExp.RegExpNFA::NFANodeAction -> Minilib.Text.RegExp.RegExpNFA::NFANodeAction`

Updates a value of union `NFANodeAction` by applying a function if it is the variant `sa_group_end`, or doing nothing otherwise.

### `mod_sa_none : (() -> ()) -> Minilib.Text.RegExp.RegExpNFA::NFANodeAction -> Minilib.Text.RegExp.RegExpNFA::NFANodeAction`

Updates a value of union `NFANodeAction` by applying a function if it is the variant `sa_none`, or doing nothing otherwise.

### `mod_sa_quant_begin : (Std::I64 -> Std::I64) -> Minilib.Text.RegExp.RegExpNFA::NFANodeAction -> Minilib.Text.RegExp.RegExpNFA::NFANodeAction`

Updates a value of union `NFANodeAction` by applying a function if it is the variant `sa_quant_begin`, or doing nothing otherwise.

### `mod_sa_quant_end : ((Std::I64, Std::I64, Std::I64) -> (Std::I64, Std::I64, Std::I64)) -> Minilib.Text.RegExp.RegExpNFA::NFANodeAction -> Minilib.Text.RegExp.RegExpNFA::NFANodeAction`

Updates a value of union `NFANodeAction` by applying a function if it is the variant `sa_quant_end`, or doing nothing otherwise.

### `mod_sa_quant_loop : (Std::I64 -> Std::I64) -> Minilib.Text.RegExp.RegExpNFA::NFANodeAction -> Minilib.Text.RegExp.RegExpNFA::NFANodeAction`

Updates a value of union `NFANodeAction` by applying a function if it is the variant `sa_quant_loop`, or doing nothing otherwise.

### `sa_assert : Minilib.Text.RegExp.RegExpPattern::PAssertion -> Minilib.Text.RegExp.RegExpNFA::NFANodeAction`

Constructs a value of union `NFANodeAction` taking the variant `sa_assert`.

### `sa_char_match : Minilib.Text.RegExp.RegExpPattern::CharClass -> Minilib.Text.RegExp.RegExpNFA::NFANodeAction`

Constructs a value of union `NFANodeAction` taking the variant `sa_char_match`.

### `sa_group_begin : Std::I64 -> Minilib.Text.RegExp.RegExpNFA::NFANodeAction`

Constructs a value of union `NFANodeAction` taking the variant `sa_group_begin`.

### `sa_group_end : Std::I64 -> Minilib.Text.RegExp.RegExpNFA::NFANodeAction`

Constructs a value of union `NFANodeAction` taking the variant `sa_group_end`.

### `sa_none : () -> Minilib.Text.RegExp.RegExpNFA::NFANodeAction`

Constructs a value of union `NFANodeAction` taking the variant `sa_none`.

### `sa_quant_begin : Std::I64 -> Minilib.Text.RegExp.RegExpNFA::NFANodeAction`

Constructs a value of union `NFANodeAction` taking the variant `sa_quant_begin`.

### `sa_quant_end : (Std::I64, Std::I64, Std::I64) -> Minilib.Text.RegExp.RegExpNFA::NFANodeAction`

Constructs a value of union `NFANodeAction` taking the variant `sa_quant_end`.

### `sa_quant_loop : Std::I64 -> Minilib.Text.RegExp.RegExpNFA::NFANodeAction`

Constructs a value of union `NFANodeAction` taking the variant `sa_quant_loop`.

## `namespace Minilib.Text.RegExp.RegExpNFA::NFAState`

### `@groups : Minilib.Text.RegExp.RegExpNFA::NFAState -> Std::Array (Std::I64, Std::I64)`

Retrieves the field `groups` from a value of `NFAState`.

### `@id : Minilib.Text.RegExp.RegExpNFA::NFAState -> Minilib.Text.RegExp.RegExpNFA::NodeID`

Retrieves the field `id` from a value of `NFAState`.

### `@quants : Minilib.Text.RegExp.RegExpNFA::NFAState -> Std::Array Std::I64`

Retrieves the field `quants` from a value of `NFAState`.

### `_sort_by_group0_begin_and_length : Std::Array Minilib.Text.RegExp.RegExpNFA::NFAState -> Std::Array Minilib.Text.RegExp.RegExpNFA::NFAState`

Sorts states by beginning of group 0 (ascending order)
and length of group 0 (descending order).

### `act_groups : [f : Std::Functor] (Std::Array (Std::I64, Std::I64) -> f (Std::Array (Std::I64, Std::I64))) -> Minilib.Text.RegExp.RegExpNFA::NFAState -> f Minilib.Text.RegExp.RegExpNFA::NFAState`

Updates a value of `NFAState` by applying a functorial action to field `groups`.

### `act_id : [f : Std::Functor] (Minilib.Text.RegExp.RegExpNFA::NodeID -> f Minilib.Text.RegExp.RegExpNFA::NodeID) -> Minilib.Text.RegExp.RegExpNFA::NFAState -> f Minilib.Text.RegExp.RegExpNFA::NFAState`

Updates a value of `NFAState` by applying a functorial action to field `id`.

### `act_quants : [f : Std::Functor] (Std::Array Std::I64 -> f (Std::Array Std::I64)) -> Minilib.Text.RegExp.RegExpNFA::NFAState -> f Minilib.Text.RegExp.RegExpNFA::NFAState`

Updates a value of `NFAState` by applying a functorial action to field `quants`.

### `collect_all_non_overlapping : Std::Array Minilib.Text.RegExp.RegExpNFA::NFAState -> Std::Array Minilib.Text.RegExp.RegExpNFA::NFAState`

Collects all non overlapping matches.

### `collect_first_match : Std::Array Minilib.Text.RegExp.RegExpNFA::NFAState -> Std::Option Minilib.Text.RegExp.RegExpNFA::NFAState`

Collects first match.

### `get_group : Std::I64 -> Minilib.Text.RegExp.RegExpNFA::NFAState -> (Std::I64, Std::I64)`

Gets specified group. If group index is out of range, returns (-1, -1).

### `get_quant : Std::I64 -> Minilib.Text.RegExp.RegExpNFA::NFAState -> Std::I64`

get quant loop count

### `group_length : Std::I64 -> Minilib.Text.RegExp.RegExpNFA::NFAState -> Std::I64`

Gets the length of specified group.

### `make : Minilib.Text.RegExp.RegExpNFA::NodeID -> Std::Array (Std::I64, Std::I64) -> Minilib.Text.RegExp.RegExpNFA::NFAState`

Creates a NFA state.

### `mod_group : Std::I64 -> ((Std::I64, Std::I64) -> (Std::I64, Std::I64)) -> Minilib.Text.RegExp.RegExpNFA::NFAState -> Minilib.Text.RegExp.RegExpNFA::NFAState`

Modify specified group.

### `mod_groups : (Std::Array (Std::I64, Std::I64) -> Std::Array (Std::I64, Std::I64)) -> Minilib.Text.RegExp.RegExpNFA::NFAState -> Minilib.Text.RegExp.RegExpNFA::NFAState`

Updates a value of `NFAState` by applying a function to field `groups`.

### `mod_id : (Minilib.Text.RegExp.RegExpNFA::NodeID -> Minilib.Text.RegExp.RegExpNFA::NodeID) -> Minilib.Text.RegExp.RegExpNFA::NFAState -> Minilib.Text.RegExp.RegExpNFA::NFAState`

Updates a value of `NFAState` by applying a function to field `id`.

### `mod_quants : (Std::Array Std::I64 -> Std::Array Std::I64) -> Minilib.Text.RegExp.RegExpNFA::NFAState -> Minilib.Text.RegExp.RegExpNFA::NFAState`

Updates a value of `NFAState` by applying a function to field `quants`.

### `overlaps : Minilib.Text.RegExp.RegExpNFA::NFAState -> Minilib.Text.RegExp.RegExpNFA::NFAState -> Std::Bool`

### `set_groups : Std::Array (Std::I64, Std::I64) -> Minilib.Text.RegExp.RegExpNFA::NFAState -> Minilib.Text.RegExp.RegExpNFA::NFAState`

Updates a value of `NFAState` by setting field `groups` to a specified one.

### `set_id : Minilib.Text.RegExp.RegExpNFA::NodeID -> Minilib.Text.RegExp.RegExpNFA::NFAState -> Minilib.Text.RegExp.RegExpNFA::NFAState`

Updates a value of `NFAState` by setting field `id` to a specified one.

### `set_quant : Std::I64 -> Std::I64 -> Minilib.Text.RegExp.RegExpNFA::NFAState -> Minilib.Text.RegExp.RegExpNFA::NFAState`

set quant loop count

### `set_quants : Std::Array Std::I64 -> Minilib.Text.RegExp.RegExpNFA::NFAState -> Minilib.Text.RegExp.RegExpNFA::NFAState`

Updates a value of `NFAState` by setting field `quants` to a specified one.

### `transition : Minilib.Text.RegExp.RegExpNFA::NodeID -> Minilib.Text.RegExp.RegExpNFA::NFAState -> Minilib.Text.RegExp.RegExpNFA::NFAState`

Makes transition to next node.

## `namespace Minilib.Text.RegExp.RegExpNFA::NFAStateSet`

### `@array : Minilib.Text.RegExp.RegExpNFA::NFAStateSet -> Std::Array Minilib.Text.RegExp.RegExpNFA::NFAState`

Retrieves the field `array` from a value of `NFAStateSet`.

### `@map : Minilib.Text.RegExp.RegExpNFA::NFAStateSet -> HashMap::HashMap Minilib.Text.RegExp.RegExpNFA::NFAState Std::Bool`

Retrieves the field `map` from a value of `NFAStateSet`.

### `act_array : [f : Std::Functor] (Std::Array Minilib.Text.RegExp.RegExpNFA::NFAState -> f (Std::Array Minilib.Text.RegExp.RegExpNFA::NFAState)) -> Minilib.Text.RegExp.RegExpNFA::NFAStateSet -> f Minilib.Text.RegExp.RegExpNFA::NFAStateSet`

Updates a value of `NFAStateSet` by applying a functorial action to field `array`.

### `act_map : [f : Std::Functor] (HashMap::HashMap Minilib.Text.RegExp.RegExpNFA::NFAState Std::Bool -> f (HashMap::HashMap Minilib.Text.RegExp.RegExpNFA::NFAState Std::Bool)) -> Minilib.Text.RegExp.RegExpNFA::NFAStateSet -> f Minilib.Text.RegExp.RegExpNFA::NFAStateSet`

Updates a value of `NFAStateSet` by applying a functorial action to field `map`.

### `add : Minilib.Text.RegExp.RegExpNFA::NFAState -> Minilib.Text.RegExp.RegExpNFA::NFAStateSet -> Minilib.Text.RegExp.RegExpNFA::NFAStateSet`

Adds a state to the state set.

### `contains : Minilib.Text.RegExp.RegExpNFA::NFAState -> Minilib.Text.RegExp.RegExpNFA::NFAStateSet -> Std::Bool`

Checks whether the state set contains a state.

### `empty : Std::I64 -> Minilib.Text.RegExp.RegExpNFA::NFAStateSet`

`NFAStateSet::empty(node_count)` creates an empty state set.
`node_count` is number of NFA nodes.

### `is_empty : Minilib.Text.RegExp.RegExpNFA::NFAStateSet -> Std::Bool`

Checks whether the state set is empty.

### `mod_array : (Std::Array Minilib.Text.RegExp.RegExpNFA::NFAState -> Std::Array Minilib.Text.RegExp.RegExpNFA::NFAState) -> Minilib.Text.RegExp.RegExpNFA::NFAStateSet -> Minilib.Text.RegExp.RegExpNFA::NFAStateSet`

Updates a value of `NFAStateSet` by applying a function to field `array`.

### `mod_map : (HashMap::HashMap Minilib.Text.RegExp.RegExpNFA::NFAState Std::Bool -> HashMap::HashMap Minilib.Text.RegExp.RegExpNFA::NFAState Std::Bool) -> Minilib.Text.RegExp.RegExpNFA::NFAStateSet -> Minilib.Text.RegExp.RegExpNFA::NFAStateSet`

Updates a value of `NFAStateSet` by applying a function to field `map`.

### `set_array : Std::Array Minilib.Text.RegExp.RegExpNFA::NFAState -> Minilib.Text.RegExp.RegExpNFA::NFAStateSet -> Minilib.Text.RegExp.RegExpNFA::NFAStateSet`

Updates a value of `NFAStateSet` by setting field `array` to a specified one.

### `set_map : HashMap::HashMap Minilib.Text.RegExp.RegExpNFA::NFAState Std::Bool -> Minilib.Text.RegExp.RegExpNFA::NFAStateSet -> Minilib.Text.RegExp.RegExpNFA::NFAStateSet`

Updates a value of `NFAStateSet` by setting field `map` to a specified one.

### `to_iter : Minilib.Text.RegExp.RegExpNFA::NFAStateSet -> Std::Iterator Minilib.Text.RegExp.RegExpNFA::NFAState`

Returns an iterator of the states.

## `namespace Minilib.Text.RegExp.RegExpNFA::NodeID`

### `@val : Minilib.Text.RegExp.RegExpNFA::NodeID -> Std::I64`

Retrieves the field `val` from a value of `NodeID`.

### `act_val : [f : Std::Functor] (Std::I64 -> f Std::I64) -> Minilib.Text.RegExp.RegExpNFA::NodeID -> f Minilib.Text.RegExp.RegExpNFA::NodeID`

Updates a value of `NodeID` by applying a functorial action to field `val`.

### `mod_val : (Std::I64 -> Std::I64) -> Minilib.Text.RegExp.RegExpNFA::NodeID -> Minilib.Text.RegExp.RegExpNFA::NodeID`

Updates a value of `NodeID` by applying a function to field `val`.

### `set_val : Std::I64 -> Minilib.Text.RegExp.RegExpNFA::NodeID -> Minilib.Text.RegExp.RegExpNFA::NodeID`

Updates a value of `NodeID` by setting field `val` to a specified one.

## `namespace Minilib.Text.RegExp.RegExpNFA::ReplaceFrag`

### `as_rep_group : Minilib.Text.RegExp.RegExpNFA::ReplaceFrag -> Std::I64`

Unwraps a union value of `ReplaceFrag` as the variant `rep_group`.
If the value is not the variant `rep_group`, this function aborts the program.

### `as_rep_literal : Minilib.Text.RegExp.RegExpNFA::ReplaceFrag -> Std::U8`

Unwraps a union value of `ReplaceFrag` as the variant `rep_literal`.
If the value is not the variant `rep_literal`, this function aborts the program.

### `is_rep_group : Minilib.Text.RegExp.RegExpNFA::ReplaceFrag -> Std::Bool`

Checks if a union value of `ReplaceFrag` is the variant `rep_group`.

### `is_rep_literal : Minilib.Text.RegExp.RegExpNFA::ReplaceFrag -> Std::Bool`

Checks if a union value of `ReplaceFrag` is the variant `rep_literal`.

### `mod_rep_group : (Std::I64 -> Std::I64) -> Minilib.Text.RegExp.RegExpNFA::ReplaceFrag -> Minilib.Text.RegExp.RegExpNFA::ReplaceFrag`

Updates a value of union `ReplaceFrag` by applying a function if it is the variant `rep_group`, or doing nothing otherwise.

### `mod_rep_literal : (Std::U8 -> Std::U8) -> Minilib.Text.RegExp.RegExpNFA::ReplaceFrag -> Minilib.Text.RegExp.RegExpNFA::ReplaceFrag`

Updates a value of union `ReplaceFrag` by applying a function if it is the variant `rep_literal`, or doing nothing otherwise.

### `rep_group : Std::I64 -> Minilib.Text.RegExp.RegExpNFA::ReplaceFrag`

Constructs a value of union `ReplaceFrag` taking the variant `rep_group`.

### `rep_literal : Std::U8 -> Minilib.Text.RegExp.RegExpNFA::ReplaceFrag`

Constructs a value of union `ReplaceFrag` taking the variant `rep_literal`.

## `namespace Minilib.Text.RegExp.RegExpNFA::Replacement`

### `_parse_dollar : Minilib.Text.SimpleParser::Parser Minilib.Text.RegExp.RegExpNFA::ReplaceFrag`

### `_parse_literal : Minilib.Text.SimpleParser::Parser Minilib.Text.RegExp.RegExpNFA::ReplaceFrag`

### `_parse_replacement_seq : Minilib.Text.SimpleParser::Parser (Std::Array Minilib.Text.RegExp.RegExpNFA::ReplaceFrag)`

### `calc_replacement : Std::String -> Std::Array Minilib.Text.RegExp.RegExpNFA::ReplaceFrag -> Minilib.Text.RegExp.RegExpNFA::NFAState -> Std::String`

Calculates actual replacement string.

### `compile : Std::String -> Std::Array Minilib.Text.RegExp.RegExpNFA::ReplaceFrag`

Compiles a replacement string to fragments.