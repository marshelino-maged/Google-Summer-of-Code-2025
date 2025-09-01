# Google Summer of Code 2025 – Work Product

![gsocXdart](https://github.com/user-attachments/assets/169a744b-e5a5-4569-9484-6e8329bc1346)

---

| Project Details |  |
|------------|-------------------------|
| **Project Title** | [Native_Doc_Dartifier: LLM-powered translation of Android (Java/Kotlin) docs into Dart using JNIgen bindings ](https://summerofcode.withgoogle.com/programs/2025/projects/8F8TuxpG) |
| **Contributor**      | [Marshelino Maged](https://github.com/marshelino-maged) |
| **Organization**     | [Dart Programming Language](https://summerofcode.withgoogle.com/programs/2025/organizations/dart) |
| **Mentors**          | [Hossein Yousefi](https://github.com/HosseinYousefi), [Daco Harkes](https://github.com/dcharkes) |
| **Project Link**    | [https://github.com/dart-lang/native/tree/main/pkgs/native_doc_dartifier](https://github.com/dart-lang/native/tree/main/pkgs/native_doc_dartifier) |

---

## 📖 Project Overview
JNIgen makes it possible to generate Dart bindings for Java and Kotlin libraries,  
But writing Dart code that interacts with these bindings is often challenging due to  
syntactic and structural differences between the languages. As a result, developers  
cannot directly reuse the numerous Java/Kotlin examples available in the official Android  
documentation and tutorials.  

This project addresses that gap by leveraging a Large Language Model (LLM) to  
automatically translate Java/Kotlin code snippets into Dart code that is fully  
compatible with JNIgen bindings. With this tool, developers can copy examples  
straight from the Android documentation and obtain equivalent Dart versions with  
minimal adjustments.  

---

## 🛠️ Work Summary
During GSoC 2025, my work focused on making Java/Kotlin → Dart translation with JNIgen more practical by combining code analysis, LLM-powered translation, and retrieval techniques. The main steps were:

- **Exploring JNIgen and Bindings**
  - Investigated how the `jnigen` package generates Dart bindings from Java/Kotlin code.
  - Compared generated Dart bindings with the original Java APIs to understand differences and challenges in translation.

- **Handling LLM Context Limitations**
  - Since the generated bindings are very large and will exceed the LLM (Gemini) context limit (~1M tokens), we designed a method to summarize them.
  - Extracted only the **public API AST** using the Dart `analyzer` package, keeping the LLM input concise and relevant.

- **Researching Best Practices**
  - Reviewed academic papers and resources on **prompting techniques**, **structured generation**, **code translation** and **error correction** to maximize LLM translation quality.
  - Studied evaluation strategies from research on **LLM testing** and **code correctness** to design reliable validation methods.


- **LLM Integration**
  - Integrated the LLM with a **structured translation prompt** for converting Java/Kotlin snippets into JNIgen-compatible Dart code.
  - Added a **retry-fix prompt** mechanism that iteratively refines the translation until all compilation errors are resolved.

- **Testing & Validation Framework**
  - Built a framework for evaluating LLM outputs, taking into account their non-deterministic nature (different outputs can still be valid).
  - Performed manual validation against real Android documentation snippets to identify edge cases and refine translation prompts.

- **Retrieval-Augmented Generation (RAG)**
  - Added RAG support to provide the LLM with only the most relevant parts of the summarized bindings.
  - Integrated ObjectBox as an embedded vector database.

---


## 📂 Contributions

### Pull Requests
| # | Title | Status |
|---|-------|--------|
| 1 | [[native_doc_dartifier] initial readme](https://github.com/dart-lang/native/pull/2308) | ✅ Merged |
| 2 | [[native_doc_dartifier] Getting Summary of Classes](https://github.com/dart-lang/native/pull/2337) | ✅ Merged |
| 3 | [[native_doc_dartifier] Extract Public API Signatures for LLM Context](https://github.com/dart-lang/native/pull/2370) | ✅ Merged |
| 4 | [[native_doc_dartifier] project set-up with an example](https://github.com/dart-lang/native/pull/2373) | ✅ Merged |
| 5 | [[native_doc_dartifier] Add initial framework for End-to-End tests](https://github.com/dart-lang/native/pull/2379) | ❌ Closed |
| 6 | [[native_doc_dartifier] Add initial framework for End-to-End tests](https://github.com/dart-lang/native/pull/2383) | ✅ Merged |
| 7 | [[native_doc_dartifier] Retry loop to fix compile errors of generated snippets](https://github.com/dart-lang/native/pull/2416) | ✅ Merged |
| 8 | [[native_doc_dartifier] Adding some End to End tests](https://github.com/dart-lang/native/pull/2420) | ✅ Merged |
| 9 | [[native_doc_dartifier] Fix format issue + Adding more test cases](https://github.com/dart-lang/native/pull/2431) | ✅ Merged |
| 10 | [[native_doc_dartifier] Experiment with large context](https://github.com/dart-lang/native/pull/2467) | ❌ Closed |
| 11 | [[native_doc_dartifier] Experiment usage of RAG in concising bindings context](https://github.com/dart-lang/native/pull/2472) | ❌ Closed |
| 12 | [[native_doc_dartifier] Fix CI](https://github.com/dart-lang/native/pull/2473) | ✅ Merged |
| 13 | [[native_doc_dartifier] Add imported packages to the context ](https://github.com/dart-lang/native/pull/2495) | ✅ Merged |
| 14 | [[native_doc_dartifier] Add more context for imported packages](https://github.com/dart-lang/native/pull/2515) | ✅ Merged |
| 15 | [[native_doc_dartifier] Improve Fixing Dart Code](https://github.com/dart-lang/native/pull/2582) | 🔄 Open |
| 16 | [Experiment ObjectBox as VectorDB for RAG](https://github.com/marshelino-maged/native/pull/16) | ❌ Closed |
| 17 | [[native_doc_dartifier] Adding RAG Option](https://github.com/dart-lang/native/pull/2584) | 🔄 Open |

---

## 🚀 Outcome
Dart developers can now more easily leverage Android documentation examples in their projects with minimal edits. This project successfully delivered a working pipeline that translates Java/Kotlin documentation snippets into JNIgen-compatible Dart code using an LLM. By addressing challenges such as large binding sizes, limited LLM context, and the non-deterministic nature of model outputs, the project introduced summarization, retry-fix prompting, and a testing flow to ensure reliability. The integration of Retrieval-Augmented Generation (RAG) further enhanced context handling, making translations more concise and accurate as a result.


---

## 🔮 Future Work
- Explore alternative RAG techniques, such as:
  - **Maximal Marginal Relevance (MMR)** for balancing relevance and diversity.  
  - **Decomposed queries** to improve retrieval quality.
  - https://github.com/dart-lang/native/issues/2550
- Build a **Chrome extension** that automatically detects Android documentation snippets and translates them into Dart.
  - https://github.com/dart-lang/native/issues/1240 
- Find a way to improve incomplete snippets translation
  - https://github.com/dart-lang/native/issues/2450 

---

## 🙏 Acknowledgements
I would like to thank my mentors, **Hossein** and **Daco**, who were the cornerstone of this project. Hossein supported me in making my very first open-source contribution, and together they guided me with advice and insights while still giving me the freedom to experiment. I learned a great deal from their approach to thinking and problem-solving, and their mentorship significantly influenced both this project and my growth as a software engineer. 

This summer has been an amazing journey, and I’m excited to keep contributing to the Dart community and beyond.

From challenges ⚡ to solutions ✅, from code 💻 to community 🤗 — GSoC 2025 was unforgettable 🚀🌱
 
---

## 📬 Contact
- GitHub: [marshelino-maged](https://github.com/marshelino-maged)  
- LinkedIn: [Marshelino Maged](https://www.linkedin.com/in/marshelino-maged-2935b91b4)  
- Email: [marshelinomaged@gmail.com](marshelinomaged@gmail.com)  
