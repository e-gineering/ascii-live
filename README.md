# ascii.live

A Go-based HTTP server for hosting ASCII animations that can be viewed directly in your terminal using `curl`. This project serves as a central hub for curl-based animations and is a follow-up to [`parrot.live`](https://github.com/hugomd/parrot.live).

## Features

- Stream ASCII animations directly to your terminal using `curl`
- Simple HTTP-based streaming with chunked transfer encoding
- Support for multiple animations with customizable frame rates
- Docker support for easy deployment
- Extensible architecture for adding new animations

## Quick Start

Try it out in your terminal:
```bash
curl ascii.live/parrot
```

<img src="./demo.gif" width="400"/>

## Available Animations

The following animations are currently available. Access any of them by using `curl ascii.live/<name>`:

| Animation Name | Command | Description |
|----------------|---------|-------------|
| parrot | `curl ascii.live/parrot` | The classic party parrot |
| nyan | `curl ascii.live/nyan` | Nyan cat animation |
| forrest | `curl ascii.live/forrest` | Run Forrest, run! |
| batman | `curl ascii.live/batman` | Batman animation |
| batman-running / bnr | `curl ascii.live/batman-running` | Batman and Robin running |
| rick | `curl ascii.live/rick` | Rick Astley (never gonna give you up) |
| can-you-hear-me | `curl ascii.live/can-you-hear-me` | Can you hear me? |
| spidyswing | `curl ascii.live/spidyswing` | Spider-Man swinging |
| torus-knot / knot | `curl ascii.live/torus-knot` | Mathematical torus knot |
| donut | `curl ascii.live/donut` | Spinning donut |
| dvd | `curl ascii.live/dvd` | DVD screensaver bounce |
| coin | `curl ascii.live/coin` | Spinning coin |
| clock / time | `curl ascii.live/clock` | Animated clock |
| bomb | `curl ascii.live/bomb` | Bomb animation |
| maxwell | `curl ascii.live/maxwell` | Maxwell the cat |
| kitty | `curl ascii.live/kitty` | Cat animation |
| earth | `curl ascii.live/earth` | Rotating Earth |
| purdue | `curl ascii.live/purdue` | Purdue animation |
| brittany | `curl ascii.live/brittany` | Brittany animation |
| india | `curl ascii.live/india` | India animation |
| as | `curl ascii.live/as` | AStrend animation |
| eg | `curl ascii.live/eg` | EG animation |
| eg90 | `curl ascii.live/eg90` | EG90 animation |

To see a JSON list of all available animations:
```bash
curl ascii.live/list
```

## Running Locally

### Prerequisites
- Go 1.17 or higher

### Running the Server
To run the server locally on port `8080`:
```bash
go run main.go
```

Then access animations at `http://localhost:8080/<animation-name>`, for example:
```bash
curl localhost:8080/parrot
```

## Running in Docker

Pull and run the latest Docker image:
```bash
docker run -p 8080:8080 hugomd/ascii-live:latest
```

Or build the Docker image yourself:
```bash
docker build -t ascii-live .
docker run -p 8080:8080 ascii-live
```

## Technical Details

### Architecture
- **Language**: Go
- **Web Framework**: Gorilla Mux for routing
- **Streaming**: HTTP chunked transfer encoding for continuous frame streaming
- **Frame Rate**: Configurable per animation (default: 70ms between frames)

### How It Works
1. Client makes a request using `curl` to a specific endpoint (e.g., `/parrot`)
2. Server validates the User-Agent contains "curl"
3. Server streams frames continuously using chunked transfer encoding
4. Each frame clears the screen and displays the next animation frame
5. Animation loops indefinitely until the client disconnects

### API Endpoints
- `GET /{frameSource}` - Stream a specific animation
- `GET /list` - Returns JSON list of all available animations

## Contributing

### Adding Frames
* [Fork this repository](https://github.com/hugomd/ascii-live/fork)
* Create a new frame file in [`/frames`](./frames), call it the name of your frames/animation, e.g. `parrot.go`
* Inside your new file, create an exported list of frames, e.g.
```Golang
package frames

// This is the value stored in the FrameMap
var MyAnimation = DefaultFrameType(myAnimationFrames)

var myAnimationFrames = []string{
  `Frame1`,
  `Frame2`,
  `Frame3`,
}
```
* In [`./frames/frames.go`](./frames/frames.go), add your animation to the `FrameMap`
* Commit and push your changes, and make a PR! If this is your first time making a PR, [check GitHub's help page on the topic](https://help.github.com/en/github/collaborating-with-issues-and-pull-requests/creating-a-pull-request)

### Guidelines for Contributions
- Ensure your animation frames are properly formatted ASCII art
- Test your animation locally before submitting
- Keep frame sizes reasonable for terminal viewing
- Follow the existing code style and structure
- Add your contribution to the Frame Contributions table below

Any animations you want to add are welcome!

## Frame Contributions
Here's a list of lovely people who have contributed frames to this project:

| Contributor                                      | Frame File                                    | Repository                                                      |
|--------------------------------------------------|-----------------------------------------------|-----------------------------------------------------------------|
| [hexrcs](https://github.com/hexrcs)              | [`forrest.go`](./frames/forrest.go)           | [`run-forrest-run`](https://github.com/hexrcs/run-forrest-run)  |
| [jmhobbs](https://github.com/jmhobbs)            | [`parrot.go`](./frames/parrot.go)             | [`terminal-parrot`](https://github.com/jmhobbs/terminal-parrot) |
| [01000001](https://github.com/01000001-01101011) | [`knot.go`](./frames/knot.go)                 | [`torus-knot`](https://github.com/01000001-01101011/torus-knot/)|

## Related Projects
* [parrot.live](https://github.com/hugomd/parrot.live) - The original party parrot streaming service
* [terminal-parrot](https://github.com/jmhobbs/terminal-parrot) - Terminal-based party parrot
* [cultofthepartyparrot.com](https://github.com/jmhobbs/cultofthepartyparrot.com) - Party parrot website
* [parrotsay](https://github.com/matheuss/parrotsay) - Like cowsay but with parrots

## License

This project is licensed under the GNU General Public License v3.0 - see the [LICENSE](LICENSE) file for details.
