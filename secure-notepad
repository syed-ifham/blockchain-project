// SPDX-License-Identifier: MIT
pragma solidity ^0.8.19;

/// @title Secure Notepad (beginner-friendly)
/// @author ChatGPT
/// @notice Simple on-chain notepad example. NOT private: data written to the blockchain is public.
/// @dev For real privacy, encrypt off-chain then store ciphertext or store content on IPFS and save the CID.
contract SecureNotepad {
    uint256 private nextId = 1;

    struct Note {
        uint256 id;
        address owner;
        string content; // store encrypted ciphertext or IPFS CID for privacy
        uint256 createdAt;
        uint256 updatedAt;
        bool exists;
    }

    // noteId => Note
    mapping(uint256 => Note) private notes;

    // noteId => (address => canRead)
    mapping(uint256 => mapping(address => bool)) private readers;

    // owner => list of note IDs (simple array for demo; in production consider more gas-efficient patterns)
    mapping(address => uint256[]) private ownerNotes;

    // events
    event NoteCreated(uint256 indexed id, address indexed owner);
    event NoteUpdated(uint256 indexed id, address indexed owner);
    event NoteDeleted(uint256 indexed id, address indexed owner);
    event NoteShared(uint256 indexed id, address indexed owner, address indexed grantee);

    modifier onlyOwner(uint256 id) {
        require(notes[id].exists, "Note does not exist");
        require(notes[id].owner == msg.sender, "Only owner can call");
        _;
    }

    /// @notice Create a new note
    /// @param content The note content, preferably encrypted or an IPFS CID
    /// @return id The id of the newly created note
    function createNote(string calldata content) external returns (uint256 id) {
        id = nextId++;
        notes[id] = Note({
            id: id,
            owner: msg.sender,
            content: content,
            createdAt: block.timestamp,
            updatedAt: block.timestamp,
            exists: true
        });
        ownerNotes[msg.sender].push(id);

        // by default owner can read
        readers[id][msg.sender] = true;

        emit NoteCreated(id, msg.sender);
    }

    /// @notice Update your note
    /// @dev Only the owner may update the note
    function updateNote(uint256 id, string calldata newContent) external onlyOwner(id) {
        notes[id].content = newContent;
        notes[id].updatedAt = block.timestamp;
        emit NoteUpdated(id, msg.sender);
    }

    /// @notice Delete your note
    /// @dev This marks it removed; content is still visible in tx history but we mark exists=false
    function deleteNote(uint256 id) external onlyOwner(id) {
        delete notes[id].content;
        notes[id].exists = false;
        emit NoteDeleted(id, msg.sender);
    }

    /// @notice Grant read access to another address
    /// @dev For privacy, you still must send them the decryption key off-chain if you used encryption
    function shareNote(uint256 id, address grantee) external onlyOwner(id) {
        readers[id][grantee] = true;
        emit NoteShared(id, msg.sender, grantee);
    }

    /// @notice Revoke read access
    function revokeShare(uint256 id, address grantee) external onlyOwner(id) {
        readers[id][grantee] = false;
        emit NoteShared(id, msg.sender, grantee); // reuse event (grantee now revoked)
    }

    /// @notice Read a note if you have permission
    /// @dev Remember: blockchain data is public. Do not put plaintext secrets on-chain.
    function readNote(uint256 id) external view returns (string memory) {
        require(notes[id].exists, "Note does not exist");
        require(readers[id][msg.sender] || notes[id].owner == msg.sender, "No read permission");
        return notes[id].content;
    }

    /// @notice Get note metadata (owner, timestamps)
    function getNoteMeta(uint256 id) external view returns (address owner, uint256 createdAt, uint256 updatedAt, bool exists) {
        Note storage n = notes[id];
        return (n.owner, n.createdAt, n.updatedAt, n.exists);
    }

    /// @notice List note IDs owned by an address
    function listMyNotes(address user) external view returns (uint256[] memory) {
        return ownerNotes[user];
    }

    // === Helper options for privacy-minded developers ===
    // Option A (recommended): Encrypt content off-chain, then store ciphertext here.
    // Option B: Store full content on IPFS/Filecoin, and save the CID in `content`.
    // Option C (not recommended): Store plaintext here — THIS IS PUBLIC.
}
