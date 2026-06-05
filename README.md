# Amazon Trust Engine

An AI-driven fraud detection and mitigation dashboard for e-commerce. It identifies and isolates fraudulent product listings using statistical modeling, graph neural network (GNN) signals, and automated agent workflows.

## Detection Models

The system evaluates trust via two primary metrics computed in real-time.

**Review-Return Discrepancy Index (RRDI)**

Measures the variance between perceived satisfaction and actual fulfillment.

```text
RRDI = | (Positive Reviews / Total Reviews) - (Successful Deliveries / Total Orders) |

```

**Trust Score**

A Bayesian-smoothed quality indicator penalized by anomalous velocity patterns.

```text
Trust Score = (Bayesian Score / 5) * 100 * (1 - Risk Factor)
Risk Factor = (0.7 * RRDI) + (0.3 * Burst Score)

```

**Intervention Rules**

* **High Risk:** `RRDI > 0.45` (Auto-block)
* **Medium Risk:** `RRDI > 0.3` AND `Burst Score > 0.5` (Flag for review)
* **Network Risk:** `GNN Signal = True` AND `RRDI > 0.2` (Flag for review)

## Architecture & Stack

* **Frontend:** Next.js 15, React 19, TypeScript, Tailwind CSS, Radix UI, Recharts
* **Backend:** Next.js API Routes, centralized in-memory datastore
* **Processing:** Human-in-the-loop agentic workflow for state mutability (blocking/unblocking)

## API Reference

System actions and data access are exposed via REST:

* `GET  /api/agent/run` — Trigger the automated fraud analysis agent.
* `POST /api/action/block` — Execute manual state override (block/unblock).
* `GET  /api/products` — Retrieve the global product dataset.
* `GET  /api/products/[asin]` — Retrieve isolated signals for a specific entity.

## Quick Start

Requires Node.js 18 or higher.

```bash
git clone <repository-url>
cd temporal-trust-engine

npm install --legacy-peer-deps
npm run dev

```

The interface is accessible at `http://localhost:3000`.

## License

MIT
