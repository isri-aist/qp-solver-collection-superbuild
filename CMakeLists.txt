AddProject(eigen-qld
  GITHUB jrl-umi3218/eigen-qld
  GIT_TAG origin/master
  NO_NINJA
)

AddProject(eigen-quadprog
  GITHUB jrl-umi3218/eigen-quadprog
  GIT_TAG origin/master
  NO_NINJA
)

AddProject(jrl-qp
  GITHUB jrl-umi3218/jrl-qp
  GIT_TAG origin/master
)

AddProject(qpOASES
  GITHUB coin-or/qpOASES
  GIT_TAG origin/master
  CMAKE_ARGS -DBUILD_SHARED_LIBS=ON
)

AddProject(osqp
  GITHUB osqp/osqp
  GIT_TAG origin/master
)

AddProject(osqp-eigen
  GITHUB robotology/osqp-eigen
  GIT_TAG origin/master
  DEPENDS osqp
)

AddProject(nasoq
  GITHUB mmurooka/nasoq
  GIT_TAG origin/cmake-install
  CMAKE_ARGS -DNASOQ_BLAS_BACKEND=OpenBLAS -DNASOQ_USE_CLAPACK=ON
)

AddProject(blasfeo
  GITHUB giaf/blasfeo
  GIT_TAG origin/master
  CMAKE_ARGS -DBUILD_SHARED_LIBS=ON -DTARGET=X64_AUTOMATIC
)

AddProject(hpipm
  GITHUB mmurooka/hpipm
  GIT_TAG origin/find-package-blasfeo
  DEPENDS blasfeo
  CMAKE_ARGS -DBUILD_SHARED_LIBS=ON
)

AddProject(proxsuite
  GITHUB Simple-Robotics/proxsuite
  GIT_TAG origin/main
  CMAKE_ARGS -DBUILD_WITH_VECTORIZATION_SUPPORT=OFF
)

AddProject(qpmad
  GITHUB asherikov/qpmad
  GIT_TAG origin/master
)

if(WITH_LSSOL)
  AddProject(eigen-lssol
    GITE multi-contact/eigen-lssol
    GIT_TAG origin/master
    NO_NINJA
  )
  set(QP_SOLVER_COLLECTION_DEPENDS_LSSOL "eigen-lssol")
else()
  set(QP_SOLVER_COLLECTION_DEPENDS_LSSOL)
endif()

AddProject(qp_solver_collection
  GITHUB isri-aist/QpSolverCollection
  GIT_TAG origin/master
  DEPENDS eigen-qld eigen-quadprog jrl-qp qpOASES osqp osqp-eigen nasoq blasfeo hpipm proxsuite qpmad ${QP_SOLVER_COLLECTION_DEPENDS_LSSOL}
  CMAKE_ARGS -DDEFAULT_ENABLE_ALL=ON -DQPOASES_INCLUDE_DIR=${CMAKE_INSTALL_PREFIX}/include -DQPOASES_LIBRARY_DIR=${CMAKE_INSTALL_PREFIX}/lib
)
