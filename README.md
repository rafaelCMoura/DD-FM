## Data Driven Fluid Mechanics (Notas de estudo)

### Capítulo 1
#### Cylinder Wake: Benchmark para Navier Stokes Incompressível


>  $\nabla \cdot \mathbf{u} = 0$
> 
> $\partial_t \mathbf{u} + \mathbf{u} \cdot \nabla \mathbf{u} = -\nabla p + \frac{1}{Re} \Delta \mathbf{u}$
>
> $`\Omega_{DNS} = \{ (x,y) \in \mathbb{R}: x^2 + y^2 \geq 1/4 \cap -10 \leq x \leq 40 \cap |y| \leq 10 \} `$

#### Mean Field Theory 🔍 
  > $\mathbf{u} = \mathbf{u_D} + \mathbf{u'}$
  > 
  > $\mathbf{u_D}(\mathbf{x}, t) = \mathbf{u_S}(\mathbf{x}) + a_{\Delta}(t)\mathbf{u}_{\Delta}(\mathbf{x})$
  > 
  > **Shift mode $\mathbf{u}_{\Delta}$**: 
  > $`\mathbf{u}_{\Delta} = (\mathbf{u}_0 - \mathbf{u_S}) / \lVert \mathbf{u}_0 - \mathbf{u_S} \rVert_{\Omega}`$
  > 
  > **Amplitude  $a_{\Delta}$**: 
  > $a_{\Delta} = (\mathbf{u}-\mathbf{u_S}, \mathbf{u}_{\Delta})$
  > 
  > **Fluctuation Energy $\mathcal{K}$**:
  > $`\mathcal{K} = \lVert \mathbf{u'} \rVert_{\Omega}^{2}/2`$

#### Feature Extraction 🔍
- ❓ **Proximity Maps with Classical Multidimensional Scaling (CMDS) $\gamma^m \in \mathbb{R}^2$**: Transforma features de alta dimensão em duas dimensões (Parecido com LLE)
  > $`\displaystyle E = \sum^{M}_{m=1} \sum^{M}_{n=1} [ \lVert \mathbf{u}^m -  \mathbf{u}^n \rVert - \lVert  \mathbf{\gamma}^m - \mathbf{\gamma}^n \rVert ]^2`$
  >
  > Para remover efeito translacional (centralizar o mapa):
  > 
  > $`\displaystyle \sum^{M}_{m=1} \mathbf{\gamma}^m = 0`$
  > 
  > Para remover efeito rotacional $`\mathbf{\gamma}^0`$ é tomado como o máximo

- **Manifold Extraction with Local Linear Embedding (LLE) $\gamma^m \in \mathbb{R}^N$**: Aproxima os snapshots por combinações lineares dos $K$ vizinhos próximos criano um manifold aproximado de menor dimensão
  > $`\displaystyle \mathbf{u}^m \approx \sum^{K}_{k=1} w_{mk} \mathbf{u}^{i_{k}^{m}}`$, e consequentemente $`\displaystyle \mathbf{\gamma}^m \approx \sum^{K}_{k=1} w_{mk} \mathbf{\gamma}^{i_{k}^{m}}`$
  >
  > Com $i_{k}^{m}$ sendo os indices dos $K$ vizinhos próximos e $w_{mk}$ pesos não negativos e o número de features $N$ escolhido até a convergência para o erro fixado


