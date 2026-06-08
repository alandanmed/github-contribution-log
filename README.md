# Contribution 1: Adapter: DeepInfra Model Provider

**Contribution Number:** 1  
**Student:** Alan Medina  
**Issue:** [Github Issue Link](https://github.com/orthogonalhq/nous-core/issues/312)
**Status:** Phase I In Progress

---

## Why I Chose This Issue

I chose this issue because it connects directly to AI tooling and model provider integration, which matches my interest in building practical AI systems beyond just using models through an interface. The issue focuses on adding support for DeepInfra as a model provider in `nous-core`, which means I would get to understand how an AI framework connects to external LLM APIs, handles requests, validates model input, supports streaming responses, and exposes the provider through the project’s existing structure.

This issue also fits my learning goals because it has a clear scope and concrete acceptance criteria. I have experience with Python, JavaScript, backend logic, API integration, and AI-focused projects, so working on an OpenAI-compatible provider feels like a good bridge between my current skills and the kind of AI infrastructure work I want to keep building toward. I also chose it because it would give me a strong portfolio story: contributing to a real open-source AI tooling project by implementing and testing a model provider adapter.

---

## Understanding the Issue

### Problem Description

The project currently does not have a DeepInfra model provider implementation. DeepInfra exposes an OpenAI-compatible `/v1/chat/completions` API, so the project needs a way to connect to DeepInfra using the existing provider architecture instead of requiring users to manually work around it. The issue asks for DeepInfra support in a way that follows the project’s existing model provider patterns.

### Expected Behavior

A user should be able to configure and use DeepInfra as a model provider inside `nous-core`. The provider should support normal model invocation, streaming responses, configuration through `getConfig`, and input validation through `TextModelInputSchema`. It should also be exported from the provider index file and covered by tests.

### Current Behavior

DeepInfra is not currently available as a supported model provider. The issue also notes that the implementation may depend on work from issue `#324`, which is refactoring a shared `ChatCompletionsProvider` primitive. Without that refactor, there may be problems caused by hard-coded OpenAI-specific environment variables like `OPENAI_API_KEY`.

### Affected Components

Likely affected files/components:

- `self/subcortex/providers/src/deepinfra-provider.ts`
- `self/subcortex/providers/src/index.ts`
- `self/subcortex/providers/src/__tests__/`
- `self/shared/src/interfaces/subcortex.ts`
- Existing provider references:
  - `openai-provider.ts`
  - `ollama-provider.ts`
  - `anthropic-provider.ts`

---

## Reproduction Process

### Environment Setup

TBD. In Phase II, I will fork the repository, clone it locally, install dependencies, and run the existing test suite. I will also inspect the current provider implementations to understand how the project structures model provider classes, configuration, streaming, and tests.

### Steps to Reproduce

1. TBD: Set up the local development environment.
2. TBD: Confirm that DeepInfra is not currently available as a provider.
3. TBD: Run existing provider tests to establish a baseline before making changes.

### Reproduction Evidence

- **Commit showing reproduction:** TBD
- **Screenshots/logs:** TBD
- **My findings:** TBD

---

## Solution Approach

### Analysis

The issue appears to require adding DeepInfra support using the project’s existing model provider pattern. Since DeepInfra uses an OpenAI-compatible chat completions API, the best solution may not be to create a completely separate adapter class from scratch. The maintainer note says this provider is intended to ship as a config entry against a shared `ChatCompletionsProvider` primitive, but that primitive is being refactored in issue `#324`. My first step will be to confirm whether `#324` has been merged or whether this issue is still blocked.

### Proposed Solution

If the `ChatCompletionsProvider` refactor is ready, I will implement DeepInfra as a provider configuration that uses the shared OpenAI-compatible chat completions logic. If the refactor is not ready, I will ask the maintainer whether they prefer waiting, working off the related branch, or using a temporary workaround. The final solution should support `invoke`, `stream`, and `getConfig`, validate inputs with `TextModelInputSchema`, export the provider, and include tests.

### Implementation Plan

Using UMPIRE framework:

**Understand:**  
The project needs DeepInfra support as an OpenAI-compatible model provider. The provider must follow the existing `IModelProvider` contract, validate inputs, support streaming, and be tested without modifying the shared provider interface or input schema.

**Match:**  
I will compare the existing provider files, especially:

- `openai-provider.ts`
- `ollama-provider.ts`
- `anthropic-provider.ts`

I will look for how they handle configuration, authentication, API calls, streaming, schema validation, exports, and tests.

**Plan:**

1. Check whether issue `#324` has been merged or whether the shared `ChatCompletionsProvider` is available.
2. Inspect existing provider implementations and tests.
3. Add DeepInfra provider support in the correct provider file or config structure.
4. Make sure authentication uses a Bearer API key.
5. Validate inputs using `TextModelInputSchema`.
6. Implement or configure support for `invoke`, `stream`, and `getConfig`.
7. Export the provider from `self/subcortex/providers/src/index.ts`.
8. Add tests under `self/subcortex/providers/src/__tests__/`.
9. Run the test suite and fix any lint/type errors.

**Implement:**  
TBD: Link to branch/commits after work begins.

**Review:**  

Self-review checklist:

- [ ] Does the implementation follow the existing provider pattern?
- [ ] Does it avoid modifying `IModelProvider`?
- [ ] Does it avoid modifying `TextModelInputSchema`?
- [ ] Does it handle streaming correctly?
- [ ] Does it validate inputs?
- [ ] Is it exported from the provider index?
- [ ] Are tests included?
- [ ] Do all tests pass locally?

**Evaluate:**  
I will verify the solution by running the existing test suite, adding DeepInfra-specific tests, and manually reviewing the behavior against the acceptance criteria from the issue.

---

## Testing Strategy

### Unit Tests

- [ ] Test case 1: DeepInfra provider returns the expected configuration.
- [ ] Test case 2: DeepInfra provider validates input using `TextModelInputSchema`.
- [ ] Test case 3: DeepInfra provider sends requests in the expected OpenAI-compatible chat completions shape.
- [ ] Test case 4: DeepInfra provider handles streaming responses correctly.
- [ ] Test case 5: DeepInfra provider handles missing or invalid API key/configuration behavior correctly.

### Integration Tests

- [ ] Integration scenario 1: Provider is exported correctly from `self/subcortex/providers/src/index.ts`.
- [ ] Integration scenario 2: Provider follows the same behavior pattern as other OpenAI-compatible providers.

### Manual Testing

TBD. If the project supports local manual provider testing, I will test a DeepInfra configuration using a sample prompt and verify that normal and streaming responses behave as expected.

---

## Implementation Notes

### Week 1 Progress

I selected issue `#312`, “Adapter: DeepInfra Model Provider,” because it matches my interest in AI infrastructure and model provider integrations. I reviewed the issue description, acceptance criteria, affected files, and maintainer note about the possible dependency on issue `#324`.

### Week 2 Progress

TBD.

### Code Changes

- **Files modified:** TBD
- **Key commits:** TBD
- **Approach decisions:** TBD

---

## Pull Request

**PR Link:** TBD

**PR Description:** TBD

Draft PR description:

This PR adds support for DeepInfra as a model provider in `nous-core`. DeepInfra uses an OpenAI-compatible chat completions API, so this implementation follows the project’s existing provider patterns while supporting invocation, streaming, configuration, input validation, exports, and tests.

**Maintainer Feedback:**

- TBD

**Status:** Not submitted yet

---

## Learnings & Reflections

### Technical Skills Gained

TBD. I expect to gain experience with LLM provider integration, OpenAI-compatible API patterns, streaming response handling, TypeScript provider interfaces, schema validation, and open-source test practices.

### Challenges Overcome

TBD. One expected challenge is understanding whether this issue is blocked by the `#324` refactor and deciding the correct implementation path based on maintainer guidance.

### What I'd Do Differently Next Time

TBD.

---

## Resources Used

- DeepInfra issue #312
- Existing provider files:
  - `openai-provider.ts`
  - `ollama-provider.ts`
  - `anthropic-provider.ts`
- `self/shared/src/interfaces/subcortex.ts`
- DeepInfra API documentation
- Project contribution guidelines
