# Module Documentation

## Module Text.Markdown.SlamDown

### Types


    data Block where
      Paragraph :: [Inline] -> Block
      Header :: Number -> [Inline] -> Block
      Blockquote :: [Block] -> Block
      List :: ListType -> [[Block]] -> Block
      CodeBlock :: CodeBlockType -> [String] -> Block
      LinkReference :: String -> String -> Block
      Rule :: Block


    data CodeBlockType where
      Indented :: CodeBlockType
      Fenced :: Boolean -> String -> CodeBlockType


    data Expr a where
      Literal :: a -> Expr a
      Evaluated :: String -> Expr a


    data FormField where
      TextBox :: TextBoxType -> Expr String -> FormField
      RadioButtons :: Expr String -> Expr [String] -> FormField
      CheckBoxes :: Expr [Boolean] -> Expr [String] -> FormField
      DropDown :: Expr [String] -> Expr String -> FormField


    data Inline where
      Str :: String -> Inline
      Entity :: String -> Inline
      Space :: Inline
      SoftBreak :: Inline
      LineBreak :: Inline
      Emph :: [Inline] -> Inline
      Strong :: [Inline] -> Inline
      Code :: Boolean -> String -> Inline
      Link :: [Inline] -> LinkTarget -> Inline
      Image :: [Inline] -> String -> Inline
      FormField :: String -> Boolean -> FormField -> Inline


    data LinkTarget where
      InlineLink :: String -> LinkTarget
      ReferenceLink :: Maybe String -> LinkTarget


    data ListType where
      Bullet :: String -> ListType
      Ordered :: String -> ListType


    data SlamDown where
      SlamDown :: [Block] -> SlamDown


    data TextBoxType where
      PlainText :: TextBoxType
      Date :: TextBoxType
      Time :: TextBoxType
      DateTime :: TextBoxType


### Type Class Instances


    instance eqListType :: Eq ListType


    instance eqSlamDown :: Eq SlamDown


    instance monoidSlamDown :: Monoid SlamDown


    instance ordSlamDown :: Ord SlamDown


    instance semigroupSlamDown :: Semigroup SlamDown


    instance showBlock :: Show Block


    instance showCodeAttr :: Show CodeBlockType


    instance showExpr :: (Show a) => Show (Expr a)


    instance showFormField :: Show FormField


    instance showInline :: Show Inline


    instance showLinkTarget :: Show LinkTarget


    instance showListType :: Show ListType


    instance showSlamDown :: Show SlamDown


    instance showTextBoxType :: Show TextBoxType


### Values


    eval :: (Maybe String -> [String] -> String) -> SlamDown -> SlamDown


    everywhere :: (Block -> Block) -> (Inline -> Inline) -> SlamDown -> SlamDown


## Module Text.Markdown.SlamDown.Parser

### Values


    parseMd :: String -> SlamDown


## Module Text.Markdown.SlamDown.Pretty

### Values


    prettyPrintMd :: SlamDown -> String


## Module Text.Markdown.SlamDown.Html

### Types


    data Html


### Values


    markdownToHtml :: String -> String


    renderHtml :: Html -> String


    toHtml :: SlamDown -> [Html]


