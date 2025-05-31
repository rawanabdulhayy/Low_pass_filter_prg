# **Low-Pass Filter Implementation**  

## **Project Overview**  
This project evaluates parallel computing approaches for implementing a **Gaussian blur (low-pass) filter** on images. We compare three computational methodologies:  
1. **Sequential Processing** (Baseline)  
2. **Multi-threaded Processing (OpenMP)**  
3. **Distributed Processing (MPI)**  

The goal is to analyze performance improvements, speedup, and efficiency when parallelizing image filtering operations.  

---

## **Team Members**  
| Name                      | ID       |
|---------------------------|----------|
| Ahmed Ibrahim Eldera      | 20P2701  |
| Mohamed Ayman Gharib      | 20P1776  |
| Rawan Ahmed Muhammed      | 20P5251  |
| Sherwet Mohamed Khalil    | 20P8105  |
| SeragEldin Mohamed Ali    | 19P1183  |


---

## **1. Introduction**  
The project focuses on implementing a **low-pass Gaussian blur filter** using different parallel computing techniques. The filter smooths images by reducing noise and high-frequency details, making it computationally intensive and ideal for parallelization.  

We analyze:  
- **Sequential processing** (baseline performance).  
- **OpenMP** (shared-memory multithreading).  
- **MPI** (distributed memory processing).  

Performance metrics include:  
✔ **Execution time**  
✔ **Speedup**  
✔ **Parallel efficiency**  

---

## **2. Methodology**  

### **2.1 Experimental Setup**  
#### **Image Filtering Operation**  
- **Kernel Size:** 7×7 Gaussian blur.  
- **Operation:** Convolves the image with a Gaussian-weighted kernel.  
- **Effect:** Smooths the image while preserving edges.  

#### **Test Configurations**  
| Method        | Configuration       | Key Features |
|--------------|---------------------|--------------|
| **Sequential** | Single-threaded | Baseline reference |
| **OpenMP**    | 4 & 8 threads | Shared-memory parallelism |
| **MPI**       | 4 & 8 processes | Distributed processing with message passing |

---

## **3. Implementation Details**  

### **3.1 Sequential Processing**  
- Single-threaded execution.  
- Serves as a baseline for speedup calculations.  
- **Code:** `sequential.cpp`  

### **3.2 OpenMP (Multi-threading)**  
- Uses `#pragma omp parallel` for workload distribution.  
- **Configurations:**  
  - **4 threads**  
  - **8 threads** (matching CPU core count)  
- **Code:** `openmp.cpp`  

### **3.3 MPI (Distributed Processing)**  
- Splits the image into chunks for parallel processing.  
- Uses **MPI_Sendrecv** for boundary exchange.  
- **Configurations:**  
  - **4 processes**  
  - **8 processes**  
- **Code:** `mpi.cpp`  

---

## **4. Performance Analysis**  

### **4.1 Execution Time Comparison**  
| Method        | Workers | Time (ms) | Speedup | Efficiency |
|--------------|---------|----------|---------|------------|
| **Sequential** | 1 | 442 | 1.00x | 100% |
| **OpenMP**    | 4 | 243 | 1.82x | 45.5% |
| **OpenMP**    | 8 | 116 | 3.81x | 47.6% |
| **MPI**      | 4 | 207 | 2.13x | 53.3% |
| **MPI**      | 8 | 105 | 4.21x | 52.6% |

### **4.2 Key Findings**  
- **OpenMP** shows near-linear speedup but lower efficiency (~47%).  
- **MPI** is more efficient (~53%) due to reduced synchronization overhead.  
- **Bottlenecks:**  
  - OpenMP: Thread synchronization.  
  - MPI: Communication overhead in boundary exchange.  

---

## **5. How to Run the Code**  

### **5.1 Compilation**  
#### **Sequential Version**  
```bash
g++ sequential.cpp -o sequential `pkg-config --cflags --libs opencv4`
```

#### **OpenMP Version**  
```bash
g++ -fopenmp openmp.cpp -o openmp `pkg-config --cflags --libs opencv4`
```

#### **MPI Version**  
```bash
mpic++ mpi.cpp -o mpi `pkg-config --cflags --libs opencv4`
```

### **5.2 Execution**  
#### **Sequential**  
```bash
./sequential
```

#### **OpenMP (4 threads)**  
```bash
./openmp
```

#### **MPI (4 processes)**  
```bash
mpirun -np 4 ./mpi
```

---

## **6. Results & Output**  
- **Input Image:** `04.jpg`  
- **Output Images:**  
  - `output_sequential.jpg`  
  - `output_openmp.jpg`  
  - `output_mpi.jpg`  

### **Sample Output**  
| Original Image | Filtered Image |
|----------------|----------------|
| ![Original](04.jpg) | ![Filtered](output_mpi.jpg) |

---

## **7. Conclusion**  
- **MPI** outperforms OpenMP in efficiency due to reduced overhead.  
- **OpenMP** is simpler but less efficient at higher thread counts.  
- **Future Work:**  
  - Hybrid MPI+OpenMP approach.  
  - GPU acceleration (CUDA).  

---

## **References**  
- OpenCV Documentation  
- MPI Standard  
- OpenMP API  

---

**© Group 40 | CSE455 - High-Performance Computing**  
**Faculty of Computers and Artificial Intelligence, Cairo University**
