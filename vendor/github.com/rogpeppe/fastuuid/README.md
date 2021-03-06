# fastuuid
--
    import "github.com/rogpeppe/fastuuid"

Package fastuuid provides fast UUID generation of 192 bit universally unique
identifiers. It does not provide formatting or parsing of the identifiers (it is
assumed that a simple hexadecimal or base64 representation is sufficient, for
which adequate functionality exists elsewhere).

Note that the generated UUIDs are not unguessable - each UUID generated from a
Generator is adjacent to the previously generated UUID.

It ignores RFC 4122.

## Usage

#### type Generator

```go
type Generator struct {
}
```

Generator represents a UUID generator that generates UUIDs in sequence from a
random starting point.

#### func  MustNewGenerator

```go
func MustNewGenerator() *Generator
```
MustNewGenerator is like NewGenerator but panics on failure.

#### func  NewGenerator

```go
func NewGenerator() (*Generator, error)
```
NewGenerator returns a new Generator. It can fail if the crypto/rand read fails.

#### func (*Generator) Next

```go
func (g *Generator) Next() [24]byte
```
Next returns the next UUID from the generator. Only the first 8 bytes can differ
from the previous UUID, so taking a slice of the first 16 bytes is sufficient to
provide a somewhat less secure 128 bit UUID.

It is OK to call this method concurrently.
