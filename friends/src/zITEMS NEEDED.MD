ITEMS WE NEED TO CREATE

[]./actions
[]    index.js
[]    addFriend

[]./components
[]    FriendItem.js
[]    FriendList.js

[]./reducers
[]    index.js
[]    friendReducer.js

[]App.js
    import { connect } from 'react-redux';
    import { addFriend } from './actions';
    import FriendList from './components/FriendList';

  []BLOCKS
    [] class App extends Component {
        constructor(props) {
          super(props);
          this.state = {
            newFriend: ''
          };
          this.addFriend = this.addFriend.bind(this);
          this.updateNewFriend = this.updateNewFriend.bind(this);
        }

      [] addFriend(event) {
          event.preventDefault();
          this.props.addFriend({
            value: this.state.newFriend,
            complete: false
          });
          this.setState({
            newFriend: ''
          });
        }

      [] updateNewFriend(event) {
          this.setState({
            newFriend: event.target.value
          });
        }

    [] render() {
          return (
            <div className="App">
              <form onSubmit={this.addFriend}>
                <input
                  onChange={this.updateNewFriend}
                  placeholder="new friend"
                  value={this.state.newFriend}
                />
              </form>
              <FriendList friends={this.props.friends} />
            </div>
          );
        }
      }

  [] const mapStateToProps = (state) => {
        return {
          friends: state.friends
        };
      };

  [] export default connect(mapStateToProps, { addFriend })(App);
