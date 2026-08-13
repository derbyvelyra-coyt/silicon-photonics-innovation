Neuromorphic Engine (NeroCore)High-performance event-driven neural simulation engine for research in mind uploading, connectomics, and Spiking Neural Networks (SNN).NeroCore is a C++20 / Rust framework designed to simulate large-scale brain architectures by balancing bio-physical accuracy with computational efficiency. Its primary goal is to bridge the gap between molecular biology and asynchronous digital processing to model emergent dynamics and evaluate state continuity (mind uploading).📸 Key FeaturesFlexible Dynamic Models: Native support for Hodgkin-Huxley (sub-cellular biophysical precision) and Izhikevich ($10\times$ speedup for large-scale simulations).Event-Driven Architecture (Spiking): Propagation of asynchronous spike trains with customizable axonal delays ($\Delta t$).Integrated Information Computation ($\Phi$): Experimental module to evaluate re-entrant network cohesion based on Integrated Information Theory (IIT).Massive Parallelism: Distributed execution across CPU/GPU using pre-computed Look-Up Tables (LUTs) to eliminate transcendental function overhead at runtime.Snapshotted State Persistence: High-performance binary serialization to freeze, pause, inspect, or transfer the full electrochemical state $S(t_0)$ of the network.🏗️ System Architecture                        ┌───────────────────────────────┐
                        │         Stimulus Input        │
                        │      I_ext / Spike Trains     │
                        └───────────────┬───────────────┘
                                        │
                                        ▼
 ┌─────────────────────────────────────────────────────────────────────────────┐
 │                       Event Queue / Spiking Scheduler                       │
 └──────┬───────────────────────────────┬───────────────────────────────┬──────┘
        │                               │                               │
        ▼                               ▼                               ▼
 ┌──────────────┐               ┌──────────────┐               ┌──────────────┐
 │   Neuron 1   │               │   Neuron 2   │               │   Neuron N   │
 │ (Izhikevich) │               │ (Izhikevich) │               │ (Hodgkin-H.) │
 └──────┬───────┘               └──────┬───────┘               └──────┬───────┘
        │                               │                               │
        └───────────────────────────────┼───────────────────────────────┘
                                        │
                                        ▼
                        ┌───────────────────────────────┐
                        │    Cohesion Evaluator (Φ)     │
                        │     Graph Mapping G(t)        │
                        └───────────────────────────────┘
🛠️ PrerequisitesC++20 Compiler (GCC 11+, Clang 13+) or Rust 1.75+CMake $3.22+$GoogleTest (for unit testing suite)CUDA Toolkit 12.0+ (Optional, for massive GPU acceleration)🚀 Installation & BuildBash# 1. Clone the repository
git clone https://github.com/your-org/nerocore.git
cd nerocore

# 2. Create build directory
mkdir build && cd build

# 3. Configure with CMake
cmake -DCMAKE_BUILD_TYPE=Release -DENABLE_CUDA=OFF ..

# 4. Build the project
make -j$(nproc)
💻 Quickstart ExampleHere is a quick example of initializing a small network of Izhikevich neurons using the engine:C++#include "nerocore/engine.hpp"
#include "nerocore/models/izhikevich.hpp"
#include <iostream>

int main() {
    // 1. Initialize simulation engine with step size dt = 0.5 ms
    nero::Engine sim(/*dt=*/0.5);

    // 2. Define parameters for a "Regular Spiking" neuron
    nero::IzhikevichConfig config{
        .a = 0.02,
        .b = 0.2,
        .c = -65.0,
        .d = 8.0
    };

    // 3. Add neuron node and inject external stimulus current (I_ext = 10.0 pA)
    auto neuron_id = sim.add_neuron(config);
    sim.set_external_current(neuron_id, 10.0);

    // 4. Run simulation for 100 ms (200 steps at dt = 0.5 ms)
    for (int step = 0; step < 200; ++step) {
        sim.step();
        
        if (sim.did_fire(neuron_id)) {
            std::cout << "[SPIKE] Detected spike at t = " << step * 0.5 << " ms" << std::endl;
        }
    }

    return 0;
